<!-- Script JS -->
<script>
  export let alumno;
  export let circleColorConverter;
  export let shadowColorConverter;
  export let internalCircleRadiusConverter;
  export let externalCircleRadiusConverter;
  export let teacherImageConverter;
  export let tdLogoConverter;
  let internalRadius = internalCircleRadiusConverter(alumno.age_1);
  let externalRadius = externalCircleRadiusConverter(alumno.age_2);

  console.log(alumno.td_rank,alumno.td_rank[0],alumno.td_rank[0].toString());
</script>

<head>
  <link rel="stylesheet" href="css/entity_styles.css" />
</head>

<!-- Estructura contenido HTML -->
<div class="column">
  <div
    class="row"
    style="margin-bottom: 40px;transform: rotate(45deg);filter: drop-shadow(0px 0px 50px {shadowColorConverter(
      alumno.language,
    )});"
  >
    {#if alumno.work_year <= 2024}
      <div class="diagonal"></div>
    {/if}
    <div class="circle external" style="margin-inline: -{externalRadius / 10}px;transform: rotate(-45deg);background-image: url({tdLogoConverter(alumno.td_rank[0].toString())});"></div>
    <div
      class="circle"
      style="width: {externalRadius}px; height:{externalRadius}px;"
    >
      <div
        class="inner-circle"
        style="width: {internalRadius}px; height:{internalRadius}px;background-color: {circleColorConverter(
          alumno.language,
        )};"
      ></div>
    </div>
    <div
      class="circle external"
      style="margin-inline: -{externalRadius /
        10}px;transform: rotate(-45deg); filter: grayscale(100%); background-image: url({teacherImageConverter(alumno.teacher)});"
    ></div>
  </div>
  <p style="padding-top: 40px;">{alumno.name}</p>
</div>

<!-- Estilos CSS -->
<style>
</style>
