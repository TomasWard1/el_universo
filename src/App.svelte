<!-- Script JS -->
<script>
  import { onMount } from "svelte";
  import Landing from "./components/Landing.svelte";
  import Entities from "./components/Entities.svelte";
</script>

<main>
  <div class="bg-animation">
    <div id="stars"></div>
    <div id="stars2"></div>
    <div id="stars3"></div>
    <div id="stars4"></div>
  </div>
  <Landing></Landing>
  <Entities></Entities>
</main>

<!-- Estilos CSS -->
<style>
</style>
