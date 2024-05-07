<!-- Script JS -->
<script>
    export let alumno;
    export let circleColorConverter;
    export let shadowColorConverter;
    let ringCount = alumno.age_2 - alumno.age_1 + 1
    let entityColor = circleColorConverter(alumno.language);
    let diffuseEntityColor = shadowColorConverter(alumno.language);
</script>

<head>
    <link rel="stylesheet" href="css/atom_styles.css" />
</head>

<!-- Estructura contenido HTML -->
<div class="atom-body">
    <div class="atom">
        <div
            class="nucleus-shadow"
            style="background: radial-gradient({entityColor} 0%, black 40%);"
        ></div>
        <div class="nucleus" style="background-color: {entityColor};"></div>
        {#each { length: ringCount} as _, i}
            <div
                class="orbit"
                style="
                width: calc(35% + {i*15}%); 
                height: calc(35% + {i*15}%);--entityColor: {diffuseEntityColor};"
            ></div>
        {/each}
        {#each { length: alumno.td_rank[0] } as _, i}
            <div
                class="electron"
                style="
                width: calc(25% + {ringCount*15}%); 
                height: calc(25% + {ringCount*15}%);
                --entityColor: {entityColor}; --tim: 15s; --pos: rotateY(20deg); --initPos: rotate({i *
                    (360 / alumno.td_rank[0])}deg); --endPos: rotate({i *
                    (360 / alumno.td_rank[0]) -
                    360}deg);"
            >
                <div
                    class="electron-background"
                    style="--entityColor: {entityColor};
                        --tim: 15s;
                        --initPos: rotateY({-1 *
                        i *
                        (360 / alumno.td_rank[0])}deg); 
                        --endPos: rotateY({-1 * i * (360 / alumno.td_rank[0]) -
                        360}deg);"
                ></div>
            </div>
        {/each}
    </div>
</div>

<!-- Estilos CSS -->
<style>
</style>
