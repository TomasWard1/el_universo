<!-- Script JS -->
<script>
    import * as d3 from "d3";
    import { onMount } from "svelte";

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
        ["#FAFF00", "FF00E5", "FFA800","FF0000","00FFF0","00FF0A"],
    );

    onMount(() => {
        d3.csv("./data/data.csv", d3.autoType).then((data) => {
            alumnos = data;
            console.log(alumnos);
        });
    });

    
</script>

<!-- Estructura contenido HTML -->

<!-- Estilos CSS -->
<style>
</style>
