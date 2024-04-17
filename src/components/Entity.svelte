<!-- Script JS -->
<script>
    import * as d3 from "d3"
    function arcGenerator({startAngle, endAngle, innerRadius, outerRadius}) {
      return d3.arc()({
        startAngle,
        endAngle,
        innerRadius,
        outerRadius,
      })
    }
  
</script>

<!-- aca se pica-->
<!-- Estructura contenido HTML -->
<main>
    <div class="persona">
        <div class="Interes">
            <svg width="200" height="200">
                <!-- ARCO DE INTERÉS -->
                <path
                    d={arcGenerator({
                    startAngle: 0,
                    endAngle: 2 * Math.PI,
                    innerRadius: 80, //VARIABLE
                    outerRadius: 100,
                    })}
                    transform="translate(100, 100)"
                />
            </svg>
        </div>
        <div class="Aprendizaje">
            <svg width="200" height="200">
            <!-- ARCO DE APRENDIZAJE -->
                <path
                    d={arcGenerator({
                    startAngle: 0,
                    endAngle: 2 * Math.PI,
                    innerRadius: 0,
                    outerRadius: 80, //VARIABLE
                    })}
                    transform="translate(100, 100)"
                />
            </svg>
        </div>
        <!-- ARCO DE LENGUAJE -->
        <!-- Contenedor LenguageProfessor -->
        <div class="Lenguage"> 
            <svg width="200" height="200">
                <path
                    id="arcPath"
                    d={arcGenerator({
                    startAngle: 0,
                    endAngle: 2 * Math.PI,
                    innerRadius: 0,
                    outerRadius: 50,
                    })}
                    fill="white"
                    transform="translate(100, 100)"
                />

                <!-- Definir el clipPath -->
              <clipPath id="arcClip">
                <use xlink:href="#arcPath" />
              </clipPath>
              <!-- Agregar la imagen con la máscara -->
              <image
                href="./images/td1Logo.svg"
                width="60"
                height="60"
                x="69"  
                y="70"
                clip-path="url(#arcClip)"
              />
            </svg>
        </div> 


        <div class="Professor">
            <svg width="200" height="200">
              <!-- Definir el arco -->
              <path
                id="arcPath1"
                d={arcGenerator({
                  startAngle: 0,
                  endAngle: 2 * Math.PI,
                  innerRadius: 0,
                  outerRadius: 50,
                })}
                fill="white"
                transform="translate(100, 100)"
              />
          
              <!-- Definir el clipPath -->
              <clipPath id="arcClip1">
                <use xlink:href="#arcPath1" />
              </clipPath>
              <!-- Agregar la imagen con la máscara -->
              <image
                href="./images/emma.png"
                width="110"
                height="110"
                x="50"  
                y="46"
                style="filter: grayscale(100%);"
                clip-path="url(#arcClip1)"
              />
            </svg>
        </div>



        <div class="Recta">
            <svg width="600" height="600">
                <!--<line x1="50" y1="150" x2="170" y2="50" stroke="white" stroke-width="2" />-->
                <line x1="0" y1="230" x2="250" y2="0" /> 
              </svg>
        </div>
    </div>    
</main>


<!-- Estilos CSS -->
<style>
    @import '../../public/css/entity_styles.css';
</style>
