<!-- Script JS -->
<script>
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
  
  <!-- transform: rotate(45deg); -->
  <div
    class="row"
    style="margin-bottom: 40px;filter: drop-shadow(0px 0px 50px {shadowColorConverter(
      alumno.language,
    )});"
  >
    <!-- {#if alumno.work_year <= 2024}
      <div class="diagonal" style="background-color: {entityColor};"></div>
    {/if} -->
    <div style="column">
      {#each { length: alumno.td_rank[0] } as _, i}
        <div
          class="circle external"
          style="margin-right: {i}px; border: 3px solid {entityColor};background-color: {entityColor};"
        ></div>
      {/each}
    </div>

    <div
      class="circle"
      style="width: {externalRadius}px; height:{externalRadius}px; border: 3px solid {entityColor}"
    >
      <div
        class="inner-circle"
        style="width: {internalRadius}px; height:{internalRadius}px;border: 3px solid {entityColor}"
      ></div>
    </div>
  </div>
  <p style="padding-top: 40px;">{alumno.name}</p>
</div>

<!-- Estilos CSS -->
<style>

</style>
