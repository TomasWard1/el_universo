<!-- Script JS -->
<script>
    import * as d3 from "d3";
    import { onMount } from "svelte";
    
    let alumnos = [];

    onMount(() => {
        d3.csv("./data/data.csv", d3.autoType).then((data) => {
            console.log(data);
        });
    });
</script>

<!-- Estructura contenido HTML -->

<!-- Estilos CSS -->
<style>
</style>
