<!-- Script JS -->
<script>
    import { onMount, onDestroy } from "svelte";
    import { writable } from "svelte/store";

    const itemsPerPage = 9; // Number of items per page
    let currentPage = writable(1); // Current page number

    let items = [];
    for (let i = 0; i < 50; i++) {
        items.push({ id: i, name: `Item ${i + 1}` });
    }

    let totalPages;
    $: {
        totalPages = Math.ceil(items.length / itemsPerPage);
    }

    onMount(() => {
        const handleKeyPress = (event) => {
            if (event.key === "ArrowLeft") {
                if ($currentPage > 1) currentPage.update((n) => n - 1);
            } else if (event.key === "ArrowRight") {
                if ($currentPage < totalPages) currentPage.update((n) => n + 1);
            }
        };

        window.addEventListener("keydown", handleKeyPress);

        return () => {
            window.removeEventListener("keydown", handleKeyPress);
        };
    });

    onDestroy(() => {
        currentPage = null; // Cleanup
    });
</script>

<!-- Estructura contenido HTML -->
<div class="fullscreen-block" style="background-color: black;">
    <div class="block-header">
        <h1>Únicos</h1>
        <p>
            "Tecnología Digital? Y esa carrera? Que es tipo ingenieria?" No, no
            somos ingenieros. Somos mucho más que eso. Programadores,
            diseñadores, emprendedores, analistas, ideadores, cuestionadores. El
            estudiante de TD pronto dominará el mundo.
        </p>
    </div>
    <div class="grid-container">
        {#each items.slice(($currentPage - 1) * itemsPerPage, $currentPage * itemsPerPage) as item}
            <div>{item.name}</div>
        {/each}
    </div>
</div>

<!-- Estilos CSS -->
<style>
    @import "../../public/css/aggregateata_styles.css";
</style>
