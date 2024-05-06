<!-- Script JS -->
<script>
    export let alumno;
    export let circleColorConverter;
    export let shadowColorConverter;
    export let internalCircleRadiusConverter;
    export let externalCircleRadiusConverter;
    let internalRadius = internalCircleRadiusConverter(alumno.age_1);
    let externalRadius = externalCircleRadiusConverter(alumno.age_2);
    let entityColor = circleColorConverter(alumno.language);
</script>

<head>
    <link rel="stylesheet" href="css/atom_styles.css" />
</head>

<!-- Estructura contenido HTML -->
<div class="atom-body">
    <div class="atom">
        <!-- <div
            class="nucleus-shadow"
            style="background: radial-gradient({entityColor} 2%, black 50%);"
        ></div> -->
        <div class="nucleus" style="background-color: {entityColor};"></div>
        <div class="orbits">
            {#each { length: alumno.td_rank[0] } as _, i}
                <div
                    class="electron"
                    style="--entityColor: {entityColor}; --tim: 7s; --pos: rotateY(20deg); --initPos: rotate({i *
                        (360 / alumno.td_rank[0])}deg); --endPos: rotate({i *
                        (360 / alumno.td_rank[0]) -
                        360}deg)"
                >
                    <div
                        class="electron-background"
                        style="--entityColor: {entityColor};
                        --pos: rotateY(20deg);
                        --tim: 7s;
                        --initPos: rotate({i *
                            (360 /
                                alumno.td_rank[0])}deg); --endPos: rotate({i *
                            (360 / alumno.td_rank[0]) -
                            360}deg)"
                    ></div>
                </div>
            {/each}
        </div>
    </div>
</div>

<!-- Estilos CSS -->
<style>
</style>
