<!-- Script JS -->
<script>
  export let alumno;
  export let circleColorConverter;
  export let teacherRuneConverter;
  export let shadowColorConverter;
  let ringCount = alumno.age_2 - alumno.age_1 + 1;
  let entityColor = circleColorConverter(alumno.language);
  let diffuseEntityColor = shadowColorConverter(alumno.language);
  let orbitTime = 15;

  function generatePlanetName(alumno) {
    let nameSub = alumno.name.substring(0, 2).toUpperCase();
    let surnameSub = alumno.name.split(" ")[1].substring(0, 2);
    let teacherSub = alumno.teacher.substring(0, 2).toUpperCase();
    let programmingLanguageSub;
    if (alumno.language == "C++") {
      programmingLanguageSub = "CEP";
    } else if (alumno.language == "C") {
      programmingLanguageSub = "CEE";
    } else {
      programmingLanguageSub = alumno.language.substring(0, 3).toUpperCase();
    }
    let ageDiff = alumno.age_2 - alumno.age_1;
    let best_td = alumno.td_rank[0];

    return `${nameSub}${surnameSub} ${teacherSub}${programmingLanguageSub} ${ageDiff}${best_td}`;
  }
</script>

<head>
  <link rel="stylesheet" href="css/planet.css" />
</head>

<!-- Estructura contenido HTML -->
<div class="column" style="scroll-snap-align: start;">
  <div class="planet-body">
    <div class="planet">
      <div
        class="nucleus-shadow"
        style="background: radial-gradient({entityColor} 0%, black 40%);"
      ></div>
      <div
        class="nucleus"
        style="background-color: {entityColor};"
      >
    <img src={teacherRuneConverter(alumno)} alt="">
        {#if alumno.work_year <= 2024}
          <svg width="987" height="987" viewBox="0 0 987 987" fill="none">
            <path
              opacity="0.5"
              fill-rule="evenodd"
              clip-rule="evenodd"
              d="M267.312 71.9688C267.312 63.7885 264.063 55.9433 258.279 50.1589C252.494 44.3746 244.649 41.125 236.469 41.125C228.288 41.125 220.443 44.3746 214.659 50.1589C208.875 55.9433 205.625 63.7885 205.625 71.9688V894.469C205.625 902.649 208.875 910.494 214.659 916.279C220.443 922.063 228.288 925.312 236.469 925.312C244.649 925.312 252.494 922.063 258.279 916.279C264.063 910.494 267.312 902.649 267.312 894.469V148.05V71.9688Z"
              fill="white"
            />
            <path
              d="M548.978 155.864L540.588 152.491C476.32 126.787 405.963 120.328 338.089 133.903L267.312 148.05V559.3L338.048 545.153C405.935 531.57 476.307 538.028 540.588 563.741C610.237 591.593 686.891 596.787 759.661 578.588L768.462 576.408C780.958 573.289 792.052 566.082 799.98 555.933C807.909 545.783 812.217 533.275 812.219 520.396V217.428C812.216 209.933 810.507 202.538 807.22 195.803C803.933 189.068 799.156 183.169 793.25 178.556C787.344 173.942 780.465 170.734 773.134 169.175C765.804 167.616 758.215 167.747 750.943 169.558C683.851 186.322 613.182 181.557 548.978 155.864Z"
              fill={entityColor}
            />
          </svg>
        {/if}
      </div>
      {#each { length: ringCount } as _, i}
        <div
          class="orbit"
          style="
                    --pos: rotateY(20deg);
                    width: calc(35% + {i * 15}%); 
                    height: calc(35% + {i *
            15}%);--entityColor: {diffuseEntityColor};"
        ></div>
      {/each}
      {#each { length: alumno.td_rank[0] } as _, i}
        <div
          class="moon"
          style="
                    width: calc(25% + {ringCount * 15}%); 
                    height: calc(25% + {ringCount * 15}%);
                    --entityColor: {entityColor}; --tim: {orbitTime}s;    --pos: rotateY(20deg); --initPos: rotate({i *
            (360 / alumno.td_rank[0])}deg); --endPos: rotate({i *
            (360 / alumno.td_rank[0]) -
            360}deg);"
        >
          <div
            class="moon-background"
            style="--entityColor: {entityColor};
                            --tim: {orbitTime}s;
                            --initPos: rotateY({-1 *
              i *
              (360 / alumno.td_rank[0])}deg); 
                            --endPos: rotateY({-1 *
              i *
              (360 / alumno.td_rank[0]) -
              360}deg);"
          ></div>
        </div>
      {/each}
    </div>
  </div>
  <h2 style="font-size: 20px; top: -80px; text-align:center; position: relative;">
    {generatePlanetName(alumno)}
  </h2>
</div>

<!-- Estilos CSS -->
<style>
</style>
