<!-- Script JS -->
<script>
    import { onMount, onDestroy } from "svelte";
    import { writable } from "svelte/store";
    import Entity from "./Entity.svelte";
    import * as d3 from "d3";

    //Cargar csv
    let alumnos = [];

    //Escalar age1 a radio del circulo interno de la entidad
    let internalCircleRadius = d3
        .scaleLinear()
        .domain([12, 18])
        .range([0, 100]);

    //Escalar age2 a radio del circulo externo de la entidad
    let externalCircleRadius = d3
        .scaleLinear()
        .domain([13, 19])
        .range([0, 100]);

    //Mapear language a el color de la sombra de la entidad
    let shadowColor = d3.scaleOrdinal(
        ["Python", "C++", "Assembler", "Swift", "Dart", "Java"],
        ["#FAFF00", "FF00E5", "FFA800", "FF0000", "00FFF0", "00FF0A"],
    );

    const itemsPerPage = 4; // Number of items per page
    let currentPage = writable(1); // Current page number

    let totalPages;
    $: {
        totalPages = Math.ceil(alumnos.length / itemsPerPage);
    }

    onMount(() => {
        d3.csv("./data/data.csv", d3.autoType).then((data) => {
            alumnos = data;
            console.log(alumnos);
        });

        const handleKeyPress = (event) => {
            if (event.key === "ArrowLeft") {
                if ($currentPage > 1) currentPage.update((n) => n - 1);
            } else if (event.key === "ArrowRight") {
                if ($currentPage < totalPages) currentPage.update((n) => n + 1);
            }
        };

        window.addEventListener("keydown", handleKeyPress);

        return () => {
            window.removeEventListener("keydown", handleKeyPress);
        };
    });

    onDestroy(() => {
        currentPage = null; // Cleanup
    });

    function gridPrev() {
        if ($currentPage > 1) currentPage.update((n) => n - 1);
    }
    function gridNext() {
        if ($currentPage < totalPages) currentPage.update((n) => n + 1);
    }
</script>

<head>
    <link rel="stylesheet" href="css/aggregated_data_styles.css" />
</head>

<!-- Estructura contenido HTML -->
<div class="fullscreen-block" style="background-color: black;">
    <div class="block-header">
        <h1>Únicos</h1>
        <p>
            "Tecnología Digital? Y esa carrera? Que es tipo ingenieria?" No, no
            somos ingenieros. Somos mucho más que eso. Programadores,
            diseñadores, emprendedores, analistas, ideadores, cuestionadores. El
            estudiante de TD pronto dominará el mundo.
        </p>
    </div>
    <div class="row">
        <button on:click={gridPrev}>Prev</button>

        <div class="grid-container">
            {#each alumnos.slice(($currentPage - 1) * itemsPerPage, $currentPage * itemsPerPage) as a}
               <Entity></Entity>
            {/each}
        </div>
        <button on:click={gridNext}>Next</button>
    </div>
</div>

<!-- Estilos CSS -->
<style>
</style>
