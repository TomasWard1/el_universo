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
  
  </div>
  <p style="padding-top: 40px;">{alumno.name}</p>
</div>

<!-- Estilos CSS -->
<style>
   .cube-wrapper {
  width: 0;
  height: 0;
  top: 100px;
  left: 100px;
  position: absolute;
  perspective-origin: 0 0;
  perspective: 80px;
}
.cube-2 {
  transform: translateZ(-100px) scaleX(1.8);
  transform-style: preserve-3d;
}
.cube {
  top: -100px;
  position: relative;
  transform-style: preserve-3d;
  animation-name: rotate;
  animation-duration: 10s;
  animation-timing-function: linear;
  animation-iteration-count: infinite;
}
@keyframes rotate {
  0% {
    transform: rotate3d(0 0, 0, 360deg);
  }
  100% {
    transform: rotate3d(0, 1, 0, 360deg);
    ;
  }
}

.face {
  position: absolute;
  background-size: 662.4px 200px;
  width: 84px;
  height: 200px;
}

#face1 {
  transform: translateX(-41.4px) translateZ(100px);
  background-position: 0 0;
}
#face2 {
  transform: translateX(29.2px) translateZ(70.8px) rotateY(45deg);
  background-position: -82.8px 0;
}
#face3 {
  transform: translateX(58.5px) rotateY(90deg);
  background-position: -165.6px 0;
}
#face4 {
  transform: translateX(29.2px) translateZ(-70.8px) rotateY(135deg);
  background-position: -248.4px 0;
}
#face5 {
  transform: translateX(-41.4px) translateZ(-100px) rotateY(180deg);
  background-position: -331.2px 0;
}
#face6 {
  transform: translateX(-111.4px) translateZ(-70.8px) rotateY(225deg);
  background-position: -414px 0;
}
#face7 {
  transform: translateX(-141.4px) rotateY(270deg);
  background-position: -496.8px 0;
}
#face8 {
  transform: translateX(-111.4px) translateZ(70px) rotateY(315deg);
  background-position: -579.6px 0;
}

.circle {
  position: absolute;
  width: 200px;
  height: 200px;
  border-radius: 50%;
}
.clip-circle {
  position: absolute;
  padding: 0;
  top: -16px;
  width: 200px;
  height: 200px;
  border-radius: 50%;
  clip-path: circle(99px at center);
}
.lighting:after {
    content: '';
    position: absolute;
    top: 50px;
    left: 67px;
}
.reflection:before {
    content: '';
    position: absolute;
    top: 0px;
    left: 0px;
    height: 200px;
    width: 200px;
    background-image:url(https://i.stack.imgur.com/ayCw7.png);
    background-size: 200px 200px;
}

.earth {
  position: absolute;
  left: 20px;
}
.earth .face{
  background-image:url(https://i.stack.imgur.com/fdtNz.jpg);
}
.earth .clip-circle {
  transform: rotateX(7deg) rotateZ(15deg);
}
.earth .lighting {
  box-shadow: -20px -30px 55px 0 rgba(0, 0, 0, 0.9) inset, -75px -100px 150px 0 rgba(0, 0, 0, 0.4) inset, 75px 100px 200px 0 rgba(255, 255, 255, 0.2) inset, -1px -2px 10px 2px rgba(200, 190, 255, 0.2);
}
.earth .lighting:after {
    box-shadow: 0 0 150px 51px rgba(255, 255, 255, 0.2), 0 0 26px 10px rgba(255, 255, 255, 0.2);
}

.wood {
  position: absolute;
  left: 240px;
}
.wood .face{
  background-image:url(https://i.stack.imgur.com/sa5P8.jpg);
}
.wood .cube-wrapper {
  transform: rotateZ(45deg);
}
.wood .lighting {
  box-shadow: -20px -30px 90px 0 rgba(0, 0, 0, 0.7) inset, -75px -100px 140px 0 rgba(0, 0, 0, 0.6) inset;
}
.wood .lighting:after {
    box-shadow: 0 0 42px 15px rgba(255, 255, 255, 0.5);
}
.wood .reflection:before {
    opacity: 0.04;
}

.metal {
  position: absolute;
  left: 460px;
}
.metal .face{
  background-image:url(https://i.stack.imgur.com/PGmVN.jpg);
}
.metal .cube-wrapper {
  transform: rotateZ(-32deg);
}
.metal .lighting {
  box-shadow: -20px -30px 100px 0 rgba(0, 0, 0, 0.9) inset, -75px -100px 107px 0 rgba(0, 0, 0, 0.3) inset, 75px 100px 127px 0 rgba(255, 255, 255, 0.23) inset;
}
.metal .lighting:after {
    box-shadow: 0 0 42px 20px rgba(255, 255, 255, 0.7), 0 0 7px 6px rgba(255, 255, 255, 0.9);
}
.metal .reflection:before {
    opacity: 0.2;
}
</style>
