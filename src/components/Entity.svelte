<!-- Script JS -->
<script>

  import Sphere from "./Sphere.svelte";

  export let alumno;
  export let circleColorConverter;
  export let shadowColorConverter;
  export let internalCircleRadiusConverter;
  export let externalCircleRadiusConverter;
  let internalRadius = internalCircleRadiusConverter(alumno.age_1);
  let externalRadius = externalCircleRadiusConverter(alumno.age_2);

  console.log(alumno.td_rank, alumno.td_rank.length);

  let entityColor = circleColorConverter(alumno.language);
</script>

<head>
  <link rel="stylesheet" href="css/entity_styles.css" />
</head>

<!-- Estructura contenido HTML -->

<div class="column">

  <div style="position:absolute;top:460px;">
    <div class="earth">
      <div class="circle lighting"></div>
    </div>

  </div>
  <div class="d-circle"></div>
  <div
    class="row"
    style="transform: rotate(45deg);margin-bottom: 40px;filter: drop-shadow(0px 0px 50px {shadowColorConverter(
      alumno.language,
    )});"
  >  <div style="column">
    {#each { length: alumno.td_rank[0] } as _, i}
      <div
        class="circle external"
        style=" border: 3px solid {entityColor};background-color: {entityColor};"
      ></div>
    {/each}
  </div>
    <div
      class="nucleus"
      style="width: {externalRadius}px; height:{externalRadius}px; border: 3px solid {entityColor}; background: radial-gradient(circle at 30% 30%, #FFFFFF 0%, #DDDDDD 20%, #888888 40%, #444444 60%, #000000 100%);"
    ></div>
    <div
      class="nucleus"
      style="width: {internalRadius}px; height:{internalRadius}px;border: 3px solid {entityColor}"
    ></div>
    <!-- {#if alumno.work_year <= 2024}
      <div class="diagonal" style="background-color: {entityColor};"></div>
    {/if} -->
    <p>
      {#if alumno.language === 'C++'}
          {alumno.teacher.substring(0, 2).toUpperCase()}{alumno.td_rank[0]}CPP
      {:else if alumno.language === 'C'}
          {alumno.teacher.substring(0, 2).toUpperCase()}{alumno.td_rank[0]}CCC
      {:else}
          {alumno.teacher.substring(0, 2).toUpperCase()}{alumno.td_rank[0]}{alumno.language.substring(0,3).toUpperCase()}
      {/if}
      </p>
  </div>
  <p style="padding-top: 40px;">{alumno.name}</p>
</div>

<!-- Estilos CSS -->
<style>

</style>
