<!-- Script JS -->
<script lang="ts">
    window.addEventListener("DOMContentLoaded", () => {
        // Define the h2 element
        const h2Element = document.querySelector("h2");

        const canvas = document.createElement("canvas");
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
        canvas.style.position = "fixed";
        canvas.style.top = "0px";
        canvas.style.left = "0px";
        canvas.style.zIndex = "-1";
        document.body.appendChild(canvas);

        const context = canvas.getContext("2d");
        const fontSize = 14;
        const columns = canvas.width / fontSize;
        const drops = [];

        for (let i = 0; i < columns; i++) {
            drops[i] = 1;
        }

        function drawMatrixRain() {
            context.fillStyle = "rgba(0, 0, 0, 0.1)";
            context.fillRect(0, 0, canvas.width, canvas.height);

            context.fillStyle = "rgba(255, 255, 255, 0.5)";
            context.font = fontSize + "px Courier";

            for (let i = 0; i < drops.length; i++) {
                // Generate a random number between 0 and 1
                const randomNumber = Math.random();
                // Convert the random number to 0 or 1 by rounding it
                const digit = Math.round(randomNumber);

                // Set the text to display based on the generated digit
                const text = digit.toString();

                const x = i * fontSize;
                let y = drops[i] * fontSize;

                context.fillText(text, x, y);

                // Reset the drop position if it goes beyond the canvas height
                if (y > canvas.height && Math.random() > 0.975) {
                    drops[i] = 0;
                }

                drops[i]++;
            }
        }

        setInterval(drawMatrixRain, 80);

        window.addEventListener("resize", () => {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        });
    });
</script>

<!-- Estructura contenido HTML -->
<div class="fullscreen-block">
    <div
        class="fade-in"
        style="display: flex;
        justify-content: center; 
        align-items: center;
    height: inherit;"
    >
        <h1 style="text-align:center">
            Una historia de los estudiantes de<br /> Tecnología Digital
        </h1>
    </div>
</div>

<!-- Estilos CSS -->
<style>
</style>
