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

  let isThemed = true;

  function handleToggle() {
    if (!isThemed) {
      isThemed = false;
    } else {
      isThemed = true;
    }
    console.log(isThemed);
    return;
  }

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

  let showPopup = false;

  function closePopup() {
    showPopup = false;
  }

  function handleKeyDown(event) {
    if (event.key === "Escape") {
      closePopup();
    }
  }
</script>

<head>
  <link rel="stylesheet" href="css/entities.css" />
</head>

<!-- Estructura contenido HTML -->
<div class="fade-in scroll-snap" style="">
  <h1 style="margin-top: 85px">{isThemed ? "NUESTRA GALAXIA" : "ALUMNOS"}</h1>
  <div class="row" style="margin-top: 30px;">
    <button
      class="button"
      style=" z-index:2;"
      on:click={() => (showPopup = true)}
    >
      <i class="fa {isThemed ? 'fa-map' : 'fa-expand'}"></i>
      {isThemed ? "Mapa" : "Leyenda"}
    </button>
    <div class="row" style="gap: 10px;">
      <label class="switch" style=" z-index:2;">
        <input
          type="checkbox"
          bind:checked={isThemed}
          on:change={handleToggle}
        />
        <span class="slider round"></span>
      </label>
      <h2 style="margin-top: 10px; z-index:2;">
        {isThemed ? "Temático" : "Aburrido"}
      </h2>
    </div>
  </div>

  {#if showPopup}
    <div
      class="popup-overlay"
      on:click={closePopup}
      on:keydown={handleKeyDown}
      tabindex="1"
      aria-label="Close Popup"
    >
      <div
        class="popup"
        on:click|stopPropagation
        tabindex="0"
        on:keydown={handleKeyDown}
        style="background-image: url('images/{isThemed
          ? 'leyenda_themed'
          : 'leyenda'}.png');"
      >
        <button class="close-button" on:click={closePopup} aria-label="Close"
          >&times;</button
        >
      </div>
    </div>
  {/if}
  <div class="grid-container">
    {#each alumnos as a}
      <Planet
        alumno={a}
        {circleColorConverter}
        {shadowColorConverter}
        {teacherRuneConverter}
        {isThemed}
      ></Planet>
    {/each}
  </div>
</div>

<!-- Estilos CSS -->
<style>
</style>
