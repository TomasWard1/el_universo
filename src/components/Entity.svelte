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
        <div class="InteresAprendizaje">
            <svg width="200" height="200">
            <!-- ARCO DE INTERÉS -->
            <path
                d={arcGenerator({
                startAngle: 0,
                endAngle: 2 * Math.PI,
                innerRadius: 80, //VARIABLE
                outerRadius: 100,
                })}
                fill="#ccc"
                transform="translate(100, 100)"
            />
            <!-- ARCO DE APRENDIZAJE -->
            <path
                d={arcGenerator({
                startAngle: 0,
                endAngle: 2 * Math.PI,
                innerRadius: 0,
                outerRadius: 80, //VARIABLE
                })}
                fill="red"
                transform="translate(100, 100)"
            />
            </svg>
        </div>
        <!-- ARCO DE LENGUAJE -->
        <!-- Contenedor LenguageProfessor -->
        <div class="Lenguage"> 
            <svg width="200" height="200">
                <path
                    d={arcGenerator({
                    startAngle: 0,
                    endAngle: 2 * Math.PI,
                    innerRadius: 0,
                    outerRadius: 50,
                    })}
                    fill="blue"
                    transform="translate(100, 100)"
                />
            </svg>
        </div> 
        <div class="Professor"> 
            <svg width="200" height="200">
                <path
                    d={arcGenerator({
                    startAngle: 0,
                    endAngle: 2 * Math.PI,
                    innerRadius: 0,
                    outerRadius: 50,
                    })}
                    fill="green"
                    transform="translate(100, 100)"
                />
            </svg>
        </div> 
        <div class="Recta">
            <svg width="500" height="500">
                <!--<line x1="50" y1="150" x2="170" y2="50" stroke="white" stroke-width="2" />-->
                <line x1="0" y1="290" x2="300" y2="0" stroke="white" stroke-width="4" /> 
              </svg>
        </div>
    </div>    
</main>


<!-- Estilos CSS -->
<style>
    @import '../../public/css/entity_styles.css';
</style>
