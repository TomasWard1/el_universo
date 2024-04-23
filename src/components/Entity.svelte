<!-- Script JS -->
<script>
  import * as d3 from "d3";

  export let alumno;
  export let shadowColorConverter;
  export let internalCircleRadiusConverter;
  export let externalCircleRadiusConverter;

  let internalRadius = internalCircleRadiusConverter(alumno.age_1);
  let externalRadius = externalCircleRadiusConverter(alumno.age_2);

  console.log(alumno.age_1, alumno.age_2, internalRadius, externalRadius);
</script>

<head>
  <link rel="stylesheet" href="css/entity_styles.css" />
</head>

<!-- aca se pica-->
<!-- Estructura contenido HTML -->
<div class="column">
  <div
    class="persona"
    style="filter: drop-shadow(2px 2px 50px {shadowColorConverter(
      alumno.language,
    )});"
  >
    <div class="circle-container">
      {#if alumno.work_year <= 2024}
        <div class="diagonal"></div>
      {/if}
      <div
        class="outer-circle"
        style="top: calc(50% - {externalRadius/2}px + {externalRadius}px * cos(45deg)); /* Adjust angle as needed */
      left: calc(50% - {externalRadius/2.4}px + {externalRadius}px * sin(45deg)); /* Adjust angle as needed */"
      ></div>
      <div
        class="inner-circle"
        style="display: inline;width:{externalRadius}px; height: {externalRadius}px;  background-color: white; justify-content: center; align-items: center;"
      ></div>
      <div
        class="inner-circle"
        style="width:{internalRadius}px; height: {internalRadius}px;  background-color: {shadowColorConverter(
          alumno.language,
        )};"
      ></div>
    </div>
  </div>
  <p style="padding-top: 40px;">{alumno.name}</p>
</div>

<!-- Estilos CSS -->
<style>
</style>
