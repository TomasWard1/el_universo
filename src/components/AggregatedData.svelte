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
        .range([30, 150]);

    // Escalar age2 a radio del circulo externo de la entidad
    let externalCircleRadius = d3
        .scaleLinear()
        .domain([12, 18])
        .range([30, 150]);

    //Mapear language a el color de la sombra de la entidad
    let shadowColorConverter = d3
        .scaleOrdinal()
        .domain(["Python", "C++", "Assembler", "Swift", "Dart", "Java", "C"])
        .range([
            "rgba(250, 255, 0, 0.7)", // #FAFF00 with 50% opacity
            "rgba(255, 0, 229, 0.7)", // #FF00E5 with 50% opacity
            "rgba(255, 168, 0, 0.7)", // #FFA800 with 50% opacity
            "rgba(255, 0, 0, 0.7)", // #FF0000 with 50% opacity
            "rgba(0, 255, 240, 0.7)", // #00FFF0 with 50% opacity
            "rgba(0, 255, 10, 0.7)", // #00FF0A with 50% opacity
            "rgba(112, 0, 255, 0.7)", // #7000FF with 50% opacity
        ]);

    let circleColorConverter = d3
        .scaleOrdinal()
        .domain(["Python", "C++", "Assembler", "Swift", "Dart", "Java", "C"])
        .range([
            "#FAFF00",
            "#FF00E5",
            "#FFA800",
            "#FF0000",
            "#00FFF0",
            "#00FF0A",
            "#7000FF",
        ]);

    let teacherImageConverter = d3
        .scaleOrdinal()
        .domain([
            "Gravano",
            "Pablo",
            "Javier",
            "Emma",
            "David",
            "Gervasio",
            "Lucio",
        ])
        .range([
            "public/images/gravano.png",
            "public/images/pablo.png",
            "public/images/javier.png",
            "public/images/emma.png",
            "public/images/david.png",
            "public/images/gerva.png",
            "public/images/lucio.png",
        ]);
        
 

        let tdLogoConverter = d3
        .scaleOrdinal()
        .domain(["1","2","3","4","5"])
        .range([
            "public/images/td1Logo.svg",
            "public/images/td2Logo.svg",
            "public/images/td3Logo.svg",
            "public/images/td4Logo.svg",
            "public/images/td5Logo.svg",
        ]);

    const itemsPerPage = 6; // Number of items per page
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
</script>

<head>
    <link rel="stylesheet" href="css/aggregated_data_styles.css" />
</head>

<!-- Estructura contenido HTML -->

<div class="fullscreen-block" style="background-color: black; height:auto">
    <div class="block-header">
        <h1>Átomos que construyen una molécula</h1>
        <p>
            "Tecnología Digital? Y esa carrera? Que es tipo ingenieria?" No, no
            somos ingenieros. Somos mucho más que eso. Programadores,
            diseñadores, emprendedores, analistas, ideadores, cuestionadores. El
            estudiante de TD pronto dominará el mundo.
        </p>
    </div>

    <div class="grid-container">
        {#each alumnos as a}
            <Entity
                alumno={a}
                {tdLogoConverter}
                {teacherImageConverter}
                {circleColorConverter}
                {shadowColorConverter}
                externalCircleRadiusConverter={externalCircleRadius}
                internalCircleRadiusConverter={internalCircleRadius}
            ></Entity>
        {/each}
    </div>
</div>

<!-- Estilos CSS -->
<style>
</style>
