<!-- Script JS -->
<script lang="ts">
  import { onMount, onDestroy } from "svelte";
  import Planet from "./Planet.svelte";
  import * as d3 from "d3";

  type Alumno = {
    age_1: number;
    age_2: number;
    language: string;
    name: string;
    td_rank: number[];
    teacher: string;
    work_year: number;
  };

  type AlumnoData = {
    age_1: number;
    age_2: number;
    language: string;
    name: string;
    td_rank: string;
    teacher: string;
    work_year: number;
  };

  //Cargar csv
  let alumnos: Alumno[] = [];

  //Mapear language a el color de la sombra de la entidad
  let shadowColorConverter = d3
    .scaleOrdinal()
    .domain(["Python", "C++", "Assembler", "Swift", "Dart", "Java", "C"])
    .range([
      "rgba(250, 255, 0, 0.5)", // #FAFF00 with 50% opacity
      "rgba(255, 0, 229, 0.5)", // #FF00E5 with 50% opacity
      "rgba(255, 168, 0, 0.5)", // #FFA800 with 50% opacity
      "rgba(255, 0, 0, 0.5)", // #FF0000 with 50% opacity
      "rgba(0, 255, 240, 0.5)", // #00FFF0 with 50% opacity
      "rgba(0, 255, 10, 0.5)", // #00FF0A with 50% opacity
      "rgba(112, 0, 255, 0.5)", // #7000FF with 50% opacity
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

  let teacherRuneConverter = d3
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
      "images/runeGravano.svg",
      "images/runePablo.svg",
      "images/runeJavi.svg",
      "images/runeEma.svg",
      "images/runeDavid.svg",
      "images/runeGerva.svg",
      "images/runeLucio.svg",
    ]);

  onMount(() => {
    d3.csv("./data/data.csv", d3.autoType).then((data) => {
      alumnos = data.map((row: AlumnoData) => {
        return {
          ...row,
          td_rank: row.td_rank.split(",").map(Number),
        };
      });

      console.log(alumnos);
    });
  });
</script>

<head>
  <link rel="stylesheet" href="css/aggregated_data_styles.css" />
</head>

<!-- Estructura contenido HTML -->
<div
  class="fade-in center"
  style="display: flex;
        scroll-snap-align: start;
   
    "
>
  <div class="grid-container">
    {#each alumnos as a}
      <Planet alumno={a} {circleColorConverter} {shadowColorConverter} {teacherRuneConverter}></Planet>
    {/each}
  </div>
</div>

<!-- Estilos CSS -->
<style>
</style>
