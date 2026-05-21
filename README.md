<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Rescate del Queltehue - Comprensión Lectora</title>
    <style>
        /* =========================================
           VARIABLES Y ESTILOS BASE
           ========================================= */
        @import url('https://fonts.googleapis.com/css2?family=Nunito:wght@400;700;900&display=swap');

        :root {
            --primary: #4CAF50;
            --primary-light: #C8E6C9;
            --primary-dark: #2E7D32;
            --secondary: #FF9800;
            --accent: #03A9F4;
            --text-dark: #333;
            --bg-color: #F3F7F9;
            --white: #FFF;
            --font-main: 'Nunito', sans-serif;
        }

        body {
            font-family: var(--font-main);
            background-color: var(--bg-color);
            color: var(--text-dark);
            margin: 0;
            padding: 0;
            line-height: 1.6;
        }

        h1, h2, h3 { color: var(--primary-dark); text-align: center; }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        /* Botones generales */
        .btn {
            font-family: var(--font-main);
            font-size: 1.2rem;
            padding: 12px 25px;
            background-color: var(--secondary);
            color: white;
            border: none;
            border-radius: 12px;
            cursor: pointer;
            box-shadow: 0 5px 0 #E65100;
            transition: 0.2s;
            font-weight: bold;
        }
        .btn:active { transform: translateY(5px); box-shadow: 0 0 0 #E65100; }
        .btn:hover { background-color: #FFA726; }
        .btn:disabled { background-color: #ccc; box-shadow: 0 5px 0 #999; cursor: not-allowed; }

        /* =========================================
           PANTALLAS (INICIO, INSTRUCCIONES, APP)
           ========================================= */
        .screen { display: none; animation: fadeIn 0.5s ease; }
        .screen.active { display: block; }

        .card {
            background: var(--white);
            border-radius: 20px;
            padding: 40px;
            text-align: center;
            box-shadow: 0 10px 25px rgba(0,0,0,0.1);
            max-width: 600px;
            margin: 50px auto;
            border: 4px solid var(--primary-light);
        }

        input[type="text"] {
            font-family: var(--font-main);
            font-size: 1.5rem;
            padding: 15px;
            border: 3px solid var(--primary-light);
            border-radius: 15px;
            width: 80%;
            margin: 20px 0;
            text-align: center;
            outline: none;
        }
        input[type="text"]:focus { border-color: var(--primary); }

        .instructions-list {
            text-align: left;
            font-size: 1.2rem;
            margin: 20px 0;
        }
        .instructions-list li { margin-bottom: 15px; }

        /* =========================================
           CABECERA Y MEDALLAS
           ========================================= */
        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: var(--white);
            padding: 15px 30px;
            border-radius: 15px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.05);
            margin-bottom: 20px;
            border-bottom: 4px solid var(--primary);
        }

        .badges-container { display: flex; gap: 15px; }
        .badge {
            opacity: 0.3;
            transition: 0.5s;
            display: flex;
            flex-direction: column;
            align-items: center;
            font-size: 2rem;
            filter: grayscale(100%);
        }
        .badge span { font-size: 0.8rem; font-weight: bold; color: var(--text-dark); }
        .badge.active { opacity: 1; transform: scale(1.1); filter: grayscale(0%); }

        /* =========================================
           ÁREA DE TRABAJO (TEXTO Y PREGUNTAS)
           ========================================= */
        .workspace {
            display: grid;
            grid-template-columns: 1.2fr 1fr;
            gap: 20px;
        }
        @media(max-width: 900px) { .workspace { grid-template-columns: 1fr; } }

        .panel {
            background: var(--white);
            padding: 25px;
            border-radius: 20px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.05);
            border: 2px solid #E0E0E0;
        }

        /* Herramientas de destacado */
        .toolbar {
            background: var(--bg-color);
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 15px;
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            align-items: center;
            border: 2px dashed #B0BEC5;
        }

        .color-btn {
            width: 35px; height: 35px;
            border-radius: 50%;
            border: 3px solid transparent;
            cursor: pointer;
            transition: 0.2s;
        }
        .color-btn.selected { border-color: #333; transform: scale(1.1); }

        select.tag-selector {
            font-family: var(--font-main);
            font-size: 1rem;
            padding: 8px;
            border-radius: 8px;
            border: 2px solid #ccc;
        }

        /* Texto y destacado */
        .reading-content, .question-header {
            font-size: 1.3rem;
            line-height: 1.8;
        }
        .vocab-box {
            background: #FFF9C4;
            padding: 15px;
            border-radius: 10px;
            margin-top: 20px;
            border-left: 5px solid #FBC02D;
        }

        .highlighted-text {
            border-radius: 5px;
            padding: 2px 4px;
            position: relative;
            font-weight: bold;
        }
        .highlight-tag {
            font-size: 0.7rem;
            background: #333;
            color: white;
            padding: 2px 5px;
            border-radius: 10px;
            vertical-align: super;
            margin-left: 4px;
        }

        /* Opciones de pregunta */
        .option-btn {
            display: block;
            width: 100%;
            text-align: left;
            padding: 15px 20px;
            margin-bottom: 12px;
            background: var(--bg-color);
            border: 3px solid #CFD8DC;
            border-radius: 12px;
            font-size: 1.2rem;
            font-family: var(--font-main);
            cursor: pointer;
            transition: 0.2s;
        }
        .option-btn:hover { background: #E1F5FE; border-color: var(--accent); }
        .option-btn.correct { background: #C8E6C9; border-color: #4CAF50; color: #1B5E20; }
        .option-btn.incorrect { background: #FFCDD2; border-color: #F44336; color: #B71C1C; }

        textarea.open-answer {
            width: 100%;
            height: 150px;
            font-family: var(--font-main);
            font-size: 1.2rem;
            padding: 15px;
            border: 3px solid #CFD8DC;
            border-radius: 12px;
            resize: vertical;
            box-sizing: border-box;
        }

        /* Feedback y Navegación */
        .feedback-box {
            margin-top: 20px;
            padding: 15px;
            border-radius: 12px;
            display: none;
            font-size: 1.1rem;
            animation: fadeIn 0.5s ease;
        }
        .feedback-box.success { background: #E8F5E9; border-left: 6px solid #4CAF50; }
        .feedback-box.error { background: #FFF3E0; border-left: 6px solid #FF9800; }

        .navigation {
            display: flex;
            justify-content: space-between;
            margin-top: 25px;
        }

        /* =========================================
           MODALES (CHECKLIST Y AUTOEVALUACIÓN)
           ========================================= */
        .modal-overlay {
            display: none;
            position: fixed;
            top: 0; left: 0; width: 100%; height: 100%;
            background: rgba(0,0,0,0.6);
            z-index: 1000;
            justify-content: center;
            align-items: center;
        }
        .modal-content {
            background: white;
            padding: 30px;
            border-radius: 20px;
            max-width: 500px;
            width: 90%;
            text-align: center;
            animation: bounceIn 0.5s;
        }
        
        .checklist-item {
            text-align: left;
            font-size: 1.2rem;
            margin: 15px 0;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        .checklist-item input[type="checkbox"] { width: 25px; height: 25px; cursor: pointer; }

        /* Estrellas */
        .star-row {
            display: flex;
            justify-content: center;
            gap: 10px;
            margin: 10px 0 20px 0;
        }
        .star { font-size: 2.5rem; color: #ccc; cursor: pointer; transition: 0.2s; }
        .star.active { color: #FFC107; }

        .eval-item { text-align: left; margin-top: 20px; font-weight: bold; }

        /* Animaciones */
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
        @keyframes bounceIn {
            0% { transform: scale(0.8); opacity: 0; }
            60% { transform: scale(1.05); opacity: 1; }
            100% { transform: scale(1); }
        }
    </style>
</head>
<body>

    <!-- PANTALLA 1: INGRESO DE NOMBRE -->
    <div id="login-screen" class="screen active">
        <div class="card">
            <h1>🐦 Rescate del Queltehue 🌿</h1>
            <p style="font-size: 1.3rem;">¡Hola! Escribe tu nombre para empezar tu misión de lectura.</p>
            <input type="text" id="student-name" placeholder="Tu nombre aquí..." />
            <br>
            <button class="btn" onclick="goToInstructions()">Siguiente ➔</button>
        </div>
    </div>

    <!-- PANTALLA 2: INSTRUCCIONES -->
    <div id="instructions-screen" class="screen">
        <div class="card">
            <h2>📜 Instrucciones para <span id="inst-name"></span></h2>
            <ul class="instructions-list">
                <li>🖍️ <strong>Usa el destacador:</strong> Selecciona palabras clave en el texto y en las preguntas usando el menú de colores.</li>
                <li>🏷️ <strong>Pon etiquetas:</strong> Usa R1, R2, etc. para marcar dónde encontraste la pista de cada pregunta.</li>
                <li>💡 <strong>Lee las pistas:</strong> Si te equivocas, no te preocupes. Te daré pistas para que vuelvas al texto a buscar la respuesta correcta.</li>
                <li>🏆 <strong>Gana medallas:</strong> Mientras más aciertes usando pistas, ganarás insignias de Detective y Maestro.</li>
            </ul>
            <button class="btn" onclick="startApp()">¡Comenzar a leer!</button>
        </div>
    </div>

    <!-- PANTALLA 3: APLICACIÓN PRINCIPAL -->
    <div id="app-screen" class="screen container">
        <header>
            <h2>👋 ¡A trabajar, <span id="display-name"></span>!</h2>
            <div class="badges-container">
                <div class="badge" id="badge-1">🔎<span>Detective</span></div>
                <div class="badge" id="badge-2">⭐<span>Buscador</span></div>
                <div class="badge" id="badge-3">🎯<span>Maestro</span></div>
            </div>
        </header>

        <div class="workspace">
            <!-- PANEL IZQUIERDO: TEXTO Y HERRAMIENTAS -->
            <div class="panel">
                <h3>📖 Texto de lectura</h3>
                
                <div class="toolbar">
                    <strong>🖍️ Destacador:</strong>
                    <div class="color-btn" style="background: #FFFF00;" onclick="selectColor('#FFFF00')"></div>
                    <div class="color-btn" style="background: #00E5FF;" onclick="selectColor('#00E5FF')"></div>
                    <div class="color-btn" style="background: #69F0AE;" onclick="selectColor('#69F0AE')"></div>
                    <div class="color-btn" style="background: #FF8A80;" onclick="selectColor('#FF8A80')"></div>
                    <div class="color-btn" style="background: #FFD180;" onclick="selectColor('#FFD180')"></div>
                    
                    <select class="tag-selector" id="tag-selector">
                        <option value="">Sin etiqueta</option>
                        <option value="R1">Pista Q1</option>
                        <option value="R2">Pista Q2</option>
                        <option value="R3">Pista Q3</option>
                        <option value="R4">Pista Q4</option>
                        <option value="R5">Pista Q5</option>
                        <option value="R6">Pista Q6</option>
                        <option value="R7">Pista Q7</option>
                        <option value="R8">Pista Q8</option>
                    </select>
                    <button class="btn" style="padding: 8px 15px; font-size: 1rem;" onclick="applyHighlight()">Destacar texto</button>
                    <button class="btn" style="padding: 8px 15px; font-size: 1rem; background: #9E9E9E; box-shadow: 0 4px 0 #616161;" onclick="clearHighlights()">Limpiar Destacados</button>
                </div>
                <p style="font-size: 0.9rem; color: #666; margin-top:-5px;"><em>💡 Selecciona texto con el mouse, elige color y etiqueta, luego haz clic en "Destacar texto". ¡Puedes destacar la pregunta también!</em></p>

                <div id="reading-text" class="reading-content">
                    <h2 style="color: black;">Queltehue salvado por jóvenes estudiantes</h2>
                    <p><em>15 de noviembre, 2026.</em></p>
                    <p><strong>Niños de una escuela ayudaron a ave nativa que agonizaba en el patio por trampa de plástico</strong></p>
                    <p>Un día extraordinario vivieron cinco estudiantes de una escuela básica en la comuna de Puente Alto, quienes salvaron de un grave peligro a un joven queltehue.</p>
                    <p>El acontecimiento empezó a eso de las 10:30 horas de la mañana de ayer, durante el recreo, cuando la profesora Carmen, quien se dirigía a la sala de profesores, avistó en el patio a un ave herida y enredada en los restos de una malla de plástico.</p>
                    <p>La profesora dio aviso de inmediato al Servicio Agrícola y Ganadero (SAG), pero mientras esperaban la ayuda —cuenta— durante casi una hora, cinco de sus alumnos se encargaron de calmar al animal. Con mucho cuidado, cortaron partes del plástico que apretaban sus alas e hidrataron sus plumas con agua fresca para protegerlas del intenso sol. Este hecho brindó al ave la oportunidad de no asfixiarse.</p>
                    <p>Luego, el equipo del SAG llegó al lugar con un veterinario, quien examinó el ejemplar y lo encontró en buenas condiciones gracias a la pronta reacción que tuvieron tanto la profesora como los estudiantes para rescatar al queltehue.</p>
                    <p>Según los últimos informes, el animal fue trasladado a un centro de rehabilitación de fauna silvestre con el fin de chequear su real estado de salud, para luego, en los próximos días, ser liberado en su hábitat natural.</p>
                    <p style="color: #666; font-size: 1rem;"><em>(Imágenes sugeridas para la diagramación: Una foto de un queltehue enredado en plástico y otra foto de un queltehue sano volando libremente).</em></p>
                    
                    <div class="vocab-box">
                        <strong>📚 Vocabulario:</strong><br>
                        • <strong>Avistó:</strong> observó a la distancia.<br>
                        • <strong>Protegerlas:</strong> cuidarlas de un daño.<br>
                        • <strong>Hábitat:</strong> lugar donde vive una especie.
                    </div>
                </div>
            </div>

            <!-- PANEL DERECHO: PREGUNTAS -->
            <div class="panel">
                <h3 style="color: var(--secondary)">📝 Pregunta <span id="question-number"></span> de 8</h3>
                
                <div id="question-text" class="question-header"></div>
                <div id="options-container"></div>
                
                <div id="feedback-area" class="feedback-box"></div>

                <div class="navigation">
                    <button class="btn" style="background:#90A4AE; box-shadow: 0 5px 0 #607D8B;" id="btn-prev" onclick="prevQuestion()">Anterior</button>
                    <button class="btn" id="btn-next" onclick="nextQuestion()">Siguiente</button>
                </div>
            </div>
        </div>
    </div>

    <!-- MODAL: CHECKLIST PREGUNTA 8 -->
    <div id="modal-checklist" class="modal-overlay">
        <div class="modal-content">
            <h2 style="color: var(--secondary);">✅ ¡Revisa tu respuesta, <span class="name-span"></span>!</h2>
            <p>Antes de guardar tu opinión, autoevalúate con este checklist:</p>
            
            <label class="checklist-item">
                <input type="checkbox" id="chk1"> ¿Tomé postura? (¿Dije claramente si estoy de acuerdo o no?)
            </label>
            <label class="checklist-item">
                <input type="checkbox" id="chk2"> ¿Repetí parte de la pregunta al iniciar mi respuesta?
            </label>
            <label class="checklist-item">
                <input type="checkbox" id="chk3"> ¿Fundamenté mi respuesta incluyendo una evidencia o pista del texto?
            </label>

            <button class="btn" style="margin-top: 20px;" onclick="saveOpinion()">¡Listo, guardar respuesta!</button>
        </div>
    </div>

    <!-- MODAL: AUTOEVALUACIÓN FINAL -->
    <div id="modal-final" class="modal-overlay">
        <div class="modal-content">
            <h2>🌟 ¡Excelente trabajo, <span class="name-span"></span>!</h2>
            <p>Has terminado las preguntas. Ahora evalúa tus estrategias de lectura pintando las estrellas (1 a 5).</p>
            
            <div class="eval-item">1. ¿Subrayé las palabras claves de las preguntas?</div>
            <div class="star-row" id="stars-1">
                <span class="star" onclick="rateStar(1, 1)">★</span><span class="star" onclick="rateStar(1, 2)">★</span><span class="star" onclick="rateStar(1, 3)">★</span><span class="star" onclick="rateStar(1, 4)">★</span><span class="star" onclick="rateStar(1, 5)">★</span>
            </div>

            <div class="eval-item">2. ¿Fui a buscar al texto la respuesta cuando no estaba seguro?</div>
            <div class="star-row" id="stars-2">
                <span class="star" onclick="rateStar(2, 1)">★</span><span class="star" onclick="rateStar(2, 2)">★</span><span class="star" onclick="rateStar(2, 3)">★</span><span class="star" onclick="rateStar(2, 4)">★</span><span class="star" onclick="rateStar(2, 5)">★</span>
            </div>

            <div class="eval-item">3. ¿Subrayé con etiquetas (R1, R2...) la pista que me ayudaba en el texto?</div>
            <div class="star-row" id="stars-3">
                <span class="star" onclick="rateStar(3, 1)">★</span><span class="star" onclick="rateStar(3, 2)">★</span><span class="star" onclick="rateStar(3, 3)">★</span><span class="star" onclick="rateStar(3, 4)">★</span><span class="star" onclick="rateStar(3, 5)">★</span>
            </div>

            <div class="eval-item">4. ¿Comprobé que la pregunta tuviera relación con lo que destaqué?</div>
            <div class="star-row" id="stars-4">
                <span class="star" onclick="rateStar(4, 1)">★</span><span class="star" onclick="rateStar(4, 2)">★</span><span class="star" onclick="rateStar(4, 3)">★</span><span class="star" onclick="rateStar(4, 4)">★</span><span class="star" onclick="rateStar(4, 5)">★</span>
            </div>

            <button class="btn" style="margin-top: 20px;" onclick="finishActivity()">¡Terminar Actividad!</button>
        </div>
    </div>

    <script>
        /* =========================================
           BASE DE DATOS DE PREGUNTAS
           ========================================= */
        const questions = [
            {
                id: 1, type: "choice", answer: 1,
                text: "¿Dónde fue encontrada el ave herida?",
                options: ["A. En el centro de rehabilitación.", "B. En el patio de la escuela.", "C. En la sala de profesores."],
                clue1: "Busca en el segundo párrafo. Dice dónde estaba la profesora Carmen cuando la avistó.",
                clue2: "Lee este fragmento: '...avistó en el ______ a un ave herida...'",
                successMsg: "¡Excelente {name}! La pista estaba en el párrafo 2: la profesora la avistó en el patio de la escuela."
            },
            {
                id: 2, type: "choice", answer: 1,
                text: "¿Por qué la profesora Carmen se contacta con el SAG?",
                options: ["A. Porque quería informar que sus alumnos no estaban en la sala.", "B. Porque quería pedir ayuda profesional para rescatar al ave herida.", "C. Porque quería felicitar a los niños por su excelente comportamiento."],
                clue1: "Piensa, si encuentras un animal herido, ¿para qué llamas a un servicio especializado?",
                clue2: "En el párrafo 3 dice que dio aviso y 'esperaban la ayuda'. Quería ayuda para el ave.",
                successMsg: "¡Muy bien pensado, {name}! Llamó al SAG para pedir ayuda profesional para rescatarla."
            },
            {
                id: 3, type: "choice", answer: 1,
                text: "¿Cuál es el propósito principal de este texto?",
                options: ["A. Enseñar los pasos para curar las alas de un ave.", "B. Informar sobre el rescate de un queltehue en una escuela.", "C. Explicar cómo viven los queltehues en la zona central."],
                clue1: "Fíjate en el formato: tiene título grande, fecha y un resumen. ¿Qué tipo de texto es?",
                clue2: "Es una noticia. El propósito de las noticias siempre es INFORMAR sobre un hecho reciente.",
                successMsg: "¡Eres muy inteligente, {name}! Como es una noticia, su propósito principal es informar sobre el rescate."
            },
            {
                id: 4, type: "choice", answer: 2,
                text: "A partir de sus acciones, ¿cuál fue la actitud de los cinco estudiantes que encontraron al queltehue?",
                options: ["A. Temerosa, porque no sabían qué hacer con el plástico.", "B. Indiferente, porque prefirieron seguir jugando en el recreo.", "C. Solidaria, porque actuaron rápido para calmar y ayudar al animal."],
                clue1: "Revisa el párrafo 3. Los niños cortaron el plástico, hidrataron sus plumas y lo calmaron.",
                clue2: "Alguien que ayuda a otro ser vivo que sufre, demuestra una actitud de compañerismo y solidaridad.",
                successMsg: "¡Exacto {name}! Fueron muy solidarios al actuar rápido para ayudarlo a no asfixiarse."
            },
            {
                id: 5, type: "choice", answer: 1,
                text: "Lee el siguiente fragmento: '...el veterinario examinó el ejemplar y lo encontró en buenas condiciones...'\n\n¿A quién se refiere la palabra subrayada (ejemplar)?",
                options: ["A. Al estudiante.", "B. Al queltehue.", "C. Al plástico."],
                clue1: "Si un veterinario examina algo para ver si está sano... ¿a quién examina?",
                clue2: "Los veterinarios curan animales, así que el 'ejemplar' es el animal rescatado.",
                successMsg: "¡Súper vocabulario, {name}! En este caso, 'ejemplar' se refiere al ave, el queltehue."
            },
            {
                id: 6, type: "choice", answer: 2,
                text: "¿De qué trata principalmente la noticia leída?",
                options: ["A. De la contaminación por plásticos que afecta a los colegios de la comuna.", "B. De cómo una profesora se dio cuenta de un accidente durante su descanso.", "C. De la oportuna acción de una comunidad escolar para salvar la vida de un ave."],
                clue1: "Piensa en toda la historia junta. ¿Cuál es el evento más importante que se cuenta de principio a fin?",
                clue2: "El titular (título) siempre resume de qué trata principalmente. Léelo de nuevo.",
                successMsg: "¡Gran capacidad de síntesis, {name}! Lo principal es la acción de los estudiantes y la profesora para salvar al ave."
            },
            {
                id: 7, type: "choice", answer: 0,
                text: "¿Para qué servirían las imágenes que acompañan a esta noticia?",
                options: ["A. Para mostrar la diferencia entre un queltehue en peligro y uno en buen estado.", "B. Para enseñar qué tipo de alimentos comen los queltehues en su hábitat.", "C. Para ilustrar cómo es el uniforme de los estudiantes que hicieron el rescate."],
                clue1: "Ve al final del texto donde dice '(Imágenes sugeridas...)'. ¿Qué dicen que mostrarían?",
                clue2: "Muestran un queltehue enredado (peligro) y otro volando libremente (buen estado).",
                successMsg: "¡Perfecto {name}! Las imágenes contrastan el peligro del plástico versus el ave sana y libre."
            },
            {
                id: 8, type: "open",
                text: "¿Estás de acuerdo con que los estudiantes hayan intentado ayudar al ave mientras llegaba el veterinario, en lugar de alejarse? Usa información del texto para responder.",
                successMsg: "¡Gracias por compartir tu opinión, {name}! Analizar la información y tomar una postura te hace un gran lector."
            }
        ];

        /* =========================================
           VARIABLES DE ESTADO
           ========================================= */
        let state = {
            name: "",
            currentIndex: 0,
            answers: {},
            attempts: {},
            points: 0,
            originalHTML: "" // Para limpiar destacados
        };

        let selectedColor = '#FFFF00';

        // Al cargar la página
        window.onload = () => {
            const saved = localStorage.getItem('queltehue_progreso');
            if(saved) {
                const parsed = JSON.parse(saved);
                if(parsed.name) {
                    state = parsed;
                    document.getElementById('student-name').value = state.name;
                }
            }
            // Guardar texto original para poder limpiar destacados
            state.originalHTML = document.getElementById('reading-text').innerHTML;
        };

        /* =========================================
           FUNCIONES DE NAVEGACIÓN Y FLUJO
           ========================================= */
        function goToInstructions() {
            const name = document.getElementById('student-name').value.trim();
            if(!name) { alert("¡Por favor, escribe tu nombre!"); return; }
            state.name = name;
            
            document.getElementById('login-screen').classList.remove('active');
            document.getElementById('instructions-screen').classList.add('active');
            document.getElementById('inst-name').textContent = state.name;
            
            // Actualizar spans en modales
            document.querySelectorAll('.name-span').forEach(el => el.textContent = state.name);
        }

        function startApp() {
            document.getElementById('instructions-screen').classList.remove('active');
            document.getElementById('app-screen').classList.add('active');
            document.getElementById('display-name').textContent = state.name;
            
            renderQuestion();
            checkBadges();
        }

        function renderQuestion() {
            const q = questions[state.currentIndex];
            document.getElementById('question-number').textContent = q.id;
            
            // Asegurar que la pregunta sea destacable envolviéndola
            document.getElementById('question-text').innerHTML = `<span id="q-content">${q.text.replace(/\n/g, "<br>")}</span>`;
            
            const optionsContainer = document.getElementById('options-container');
            const feedbackArea = document.getElementById('feedback-area');
            
            optionsContainer.innerHTML = '';
            feedbackArea.style.display = 'none';
            feedbackArea.className = 'feedback-box';

            if(q.type === "choice") {
                q.options.forEach((opt, index) => {
                    const btn = document.createElement('button');
                    btn.className = 'option-btn';
                    btn.textContent = opt;
                    
                    if (state.answers[q.id] !== undefined) {
                        btn.disabled = true;
                        if(index === q.answer) btn.classList.add('correct');
                        if(state.answers[q.id] === index && index !== q.answer) btn.classList.add('incorrect');
                    } else {
                        btn.onclick = () => handleAnswer(q, index, btn);
                    }
                    optionsContainer.appendChild(btn);
                });

                if (state.answers[q.id] === q.answer) {
                    showFeedback(q.successMsg.replace('{name}', state.name), 'success');
                }
            } else if (q.type === "open") {
                const textarea = document.createElement('textarea');
                textarea.className = 'open-answer';
                textarea.id = 'opinion-text';
                textarea.placeholder = "Escribe tu respuesta aquí basándote en el texto...";
                if(state.answers[q.id]) textarea.value = state.answers[q.id];
                
                const saveBtn = document.createElement('button');
                saveBtn.className = 'btn';
                saveBtn.style.marginTop = '15px';
                saveBtn.textContent = 'Terminar Respuesta';
                
                if (state.answers[q.id]) {
                    textarea.disabled = true;
                    saveBtn.style.display = 'none';
                    showFeedback(q.successMsg.replace('{name}', state.name), 'success');
                } else {
                    saveBtn.onclick = () => {
                        if(textarea.value.trim().length < 10) {
                            alert("Por favor, escribe una respuesta un poco más completa.");
                            return;
                        }
                        // Abrir modal de checklist
                        document.getElementById('modal-checklist').style.display = 'flex';
                    };
                }

                optionsContainer.appendChild(textarea);
                optionsContainer.appendChild(saveBtn);
            }

            // Botones de navegación
            document.getElementById('btn-prev').style.visibility = (state.currentIndex === 0) ? 'hidden' : 'visible';
            document.getElementById('btn-next').textContent = (state.currentIndex === questions.length - 1) ? 'Finalizar' : 'Siguiente';
            
            // Auto seleccionar etiqueta R correspondiente
            document.getElementById('tag-selector').value = `R${q.id}`;
        }

        /* =========================================
           LÓGICA DE RESPUESTAS Y FEEDBACK
           ========================================= */
        function handleAnswer(q, selectedIndex, btnElement) {
            if (!state.attempts[q.id]) state.attempts[q.id] = 0;
            state.attempts[q.id]++;

            const allBtns = document.querySelectorAll('.option-btn');
            
            if (selectedIndex === q.answer) {
                // CORRECTO
                btnElement.classList.add('correct');
                state.answers[q.id] = selectedIndex;
                if (state.attempts[q.id] === 1) state.points += 2;
                else state.points += 1;
                
                showFeedback(q.successMsg.replace('{name}', state.name), 'success');
                allBtns.forEach(b => b.disabled = true);
                saveProgress();
                checkBadges();
            } else {
                // INCORRECTO
                btnElement.classList.add('incorrect');
                
                let feedbackMsg = "";
                if (state.attempts[q.id] === 1) {
                    feedbackMsg = `¡Casi, ${state.name}! Pista 1: ${q.clue1} Vuelve al texto a destacar la pista.`;
                } else {
                    feedbackMsg = `Tranquilo ${state.name}, intenta de nuevo. Pista 2: ${q.clue2}`;
                }
                showFeedback(feedbackMsg, 'error');
            }
        }

        function showFeedback(message, type) {
            const fb = document.getElementById('feedback-area');
            fb.textContent = message;
            fb.className = 'feedback-box ' + type;
            fb.style.display = 'block';
        }

        /* =========================================
           CHECKLIST DE OPINIÓN (PREGUNTA 8)
           ========================================= */
        function saveOpinion() {
            const c1 = document.getElementById('chk1').checked;
            const c2 = document.getElementById('chk2').checked;
            const c3 = document.getElementById('chk3').checked;
            
            if(!c1 || !c2 || !c3) {
                alert(`¡Hola ${state.name}! Intenta marcar todas las casillas para asegurarte de que tu respuesta está súper completa.`);
                return;
            }

            const text = document.getElementById('opinion-text').value;
            state.answers[8] = text;
            state.points += 2;
            
            document.getElementById('modal-checklist').style.display = 'none';
            saveProgress();
            checkBadges();
            renderQuestion(); // Para deshabilitar la textarea y mostrar éxito
        }

        /* =========================================
           NAVEGACIÓN ENTRE PREGUNTAS
           ========================================= */
        function nextQuestion() {
            if (state.currentIndex < questions.length - 1) {
                state.currentIndex++;
                renderQuestion();
                saveProgress();
            } else {
                // Al presionar Finalizar en la última pregunta
                if(!state.answers[8]) {
                    alert("¡Te falta responder la última pregunta de opinión!");
                    return;
                }
                document.getElementById('modal-final').style.display = 'flex';
            }
        }

        function prevQuestion() {
            if (state.currentIndex > 0) {
                state.currentIndex--;
                renderQuestion();
                saveProgress();
            }
        }

        /* =========================================
           SISTEMA DE INSIGNIAS Y GUARDADO
           ========================================= */
        function checkBadges() {
            let correctCount = Object.keys(state.answers).length;
            if (correctCount >= 3) document.getElementById('badge-1').classList.add('active');
            if (correctCount >= 6) document.getElementById('badge-2').classList.add('active');
            if (correctCount >= 8) document.getElementById('badge-3').classList.add('active');
        }

        function saveProgress() {
            localStorage.setItem('queltehue_progreso', JSON.stringify(state));
        }

        /* =========================================
           HERRAMIENTAS DE DESTACADO
           ========================================= */
        function selectColor(color) {
            selectedColor = color;
            document.querySelectorAll('.color-btn').forEach(btn => {
                btn.classList.remove('selected');
                // Convert to hex or rgb for comparison
                if(btn.style.background === color || btn.style.backgroundColor === color || btn.style.backgroundColor === hexToRgb(color)) {
                    btn.classList.add('selected');
                }
            });
        }
        selectColor('#FFFF00');

        // Función de ayuda para comparar colores en DOM
        function hexToRgb(hex) {
            var result = /^#?([a-f\d]{2})([a-f\d]{2})([a-f\d]{2})$/i.exec(hex);
            return result ? `rgb(${parseInt(result[1], 16)}, ${parseInt(result[2], 16)}, ${parseInt(result[3], 16)})` : null;
        }

        function applyHighlight() {
            const selection = window.getSelection();
            if (!selection.rangeCount || selection.isCollapsed) {
                alert(`¡Hola ${state.name}! Primero debes seleccionar con tu mouse las palabras en el texto o en la pregunta.`);
                return;
            }

            const range = selection.getRangeAt(0);
            
            // Validar que se está destacando dentro del área de texto o de la pregunta
            const readingNode = document.getElementById('reading-text');
            const questionNode = document.getElementById('question-text');
            
            if (!readingNode.contains(range.commonAncestorContainer) && !questionNode.contains(range.commonAncestorContainer)) {
                 return; 
            }

            try {
                const span = document.createElement('span');
                span.className = 'highlighted-text';
                span.style.backgroundColor = selectedColor;

                const tagValue = document.getElementById('tag-selector').value;
                if(tagValue !== "") {
                    const tag = document.createElement('span');
                    tag.className = 'highlight-tag';
                    tag.textContent = tagValue;
                    
                    const content = range.extractContents();
                    span.appendChild(content);
                    span.appendChild(tag);
                } else {
                    const content = range.extractContents();
                    span.appendChild(content);
                }

                range.insertNode(span);
                selection.removeAllRanges();
            } catch(e) {
                alert("Para que funcione mejor, intenta destacar frases de un solo párrafo a la vez.");
            }
        }

        function clearHighlights() {
            if(confirm("¿Seguro que quieres borrar todo lo destacado en el texto?")) {
                document.getElementById('reading-text').innerHTML = state.originalHTML;
            }
        }

        /* =========================================
           AUTOEVALUACIÓN FINAL (ESTRELLAS)
           ========================================= */
        let finalRatings = { 1: 0, 2: 0, 3: 0, 4: 0 };

        function rateStar(questionNum, starVal) {
            finalRatings[questionNum] = starVal;
            const container = document.getElementById(`stars-${questionNum}`);
            const stars = container.querySelectorAll('.star');
            
            stars.forEach((s, index) => {
                if (index < starVal) s.classList.add('active');
                else s.classList.remove('active');
            });
        }

        function finishActivity() {
            // Verificar que todas tengan estrellas
            if(Object.values(finalRatings).includes(0)) {
                alert("Por favor, pinta las estrellas en todas las preguntas antes de terminar.");
                return;
            }
            
            document.getElementById('modal-final').style.display = 'none';
            alert(`¡Felicidades, ${state.name}! Has completado toda la actividad con éxito y has obtenido ${state.points} puntos de investigador.\n¡Eres un Maestro Lector! 🎯`);
            
            // Opcional: limpiar localStorage para que el siguiente alumno empiece de cero
            // localStorage.removeItem('queltehue_progreso');
        }
    </script>
</body>
</html>
