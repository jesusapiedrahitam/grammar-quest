<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Grammar Quest Champions</title>
    <style>
        :root {
            --primary: #4361ee;
            --secondary: #3a0ca3;
            --accent: #f72585;
            --light: #f8f9fa;
            --dark: #212529;
            --success: #4cc9f0;
            --warning: #ffba08;
            --danger: #f94144;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
            color: var(--light);
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 20px;
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.2);
        }
        
        header {
            text-align: center;
            margin-bottom: 30px;
            padding: 20px;
        }
        
        h1 {
            font-size: 3rem;
            margin-bottom: 10px;
            color: white;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
        }
        
        .subtitle {
            font-size: 1.2rem;
            opacity: 0.9;
        }
        
        .game-screen {
            display: none;
            animation: fadeIn 0.5s ease;
        }
        
        #lobby {
            display: block;
        }
        
        .screen-title {
            text-align: center;
            margin-bottom: 20px;
            color: white;
        }
        
        .player-form {
            background: rgba(255, 255, 255, 0.15);
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 20px;
            text-align: center;
        }
        
        input, button, select {
            padding: 12px 15px;
            border: none;
            border-radius: 50px;
            margin: 5px;
            font-size: 1rem;
        }
        
        input, select {
            width: 250px;
            background: rgba(255, 255, 255, 0.9);
            color: var(--dark);
        }
        
        button {
            background: var(--primary);
            color: white;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: bold;
        }
        
        button:hover {
            background: var(--secondary);
            transform: translateY(-2px);
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        }
        
        button:disabled {
            background: #6c757d;
            cursor: not-allowed;
            transform: none;
            box-shadow: none;
        }
        
        .avatar-selection {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            justify-content: center;
            margin: 15px 0;
        }
        
        .avatar-option {
            width: 60px;
            height: 60px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
            cursor: pointer;
            transition: all 0.3s ease;
            border: 3px solid transparent;
        }
        
        .avatar-option:hover {
            transform: scale(1.1);
        }
        
        .avatar-option.selected {
            border-color: var(--warning);
            transform: scale(1.1);
        }
        
        .players-container {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            justify-content: center;
            margin: 20px 0;
        }
        
        .player-card {
            background: rgba(255, 255, 255, 0.2);
            border-radius: 15px;
            padding: 15px;
            width: 150px;
            text-align: center;
            transition: all 0.3s ease;
        }
        
        .player-card:hover {
            transform: translateY(-5px);
            background: rgba(255, 255, 255, 0.25);
        }
        
        .player-avatar {
            width: 60px;
            height: 60px;
            border-radius: 50%;
            margin: 0 auto 10px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
            font-weight: bold;
        }
        
        .game-container {
            display: grid;
            grid-template-columns: 2fr 1fr;
            gap: 20px;
        }
        
        .question-box {
            background: rgba(255, 255, 255, 0.15);
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 20px;
            position: relative;
        }
        
        .question-text {
            font-size: 1.4rem;
            margin-bottom: 20px;
            text-align: center;
        }
        
        .options-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
        }
        
        .option-btn {
            padding: 15px;
            text-align: left;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 10px;
            border: 2px solid transparent;
            cursor: pointer;
            transition: all 0.3s ease;
            color: white;
            font-size: 1rem;
        }
        
        .option-btn:hover {
            background: rgba(255, 255, 255, 0.2);
            border-color: var(--primary);
        }
        
        .timer-container {
            text-align: center;
            margin: 20px 0;
        }
        
        .timer {
            font-size: 2.5rem;
            font-weight: bold;
            color: white;
        }
        
        .score-board {
            background: rgba(255, 255, 255, 0.15);
            padding: 20px;
            border-radius: 15px;
            max-height: 500px;
            overflow-y: auto;
        }
        
        .score-title {
            text-align: center;
            margin-bottom: 15px;
            color: white;
        }
        
        .score-item {
            display: flex;
            justify-content: space-between;
            padding: 10px;
            background: rgba(255, 255, 255, 0.1);
            margin-bottom: 10px;
            border-radius: 10px;
            animation: slideIn 0.3s ease;
        }
        
        .score-item.highlight {
            background: rgba(76, 201, 240, 0.3);
            transform: scale(1.02);
        }
        
        .level-indicator {
            text-align: center;
            margin: 15px 0;
            font-size: 1.2rem;
        }
        
        .results-container {
            text-align: center;
        }
        
        .winner-badge {
            font-size: 2rem;
            color: var(--warning);
            margin: 20px 0;
            animation: pulse 1.5s infinite;
        }
        
        .progress-bar {
            height: 20px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 10px;
            margin: 20px 0;
            overflow: hidden;
        }
        
        .progress {
            height: 100%;
            background: var(--success);
            border-radius: 10px;
            transition: width 0.5s ease;
        }
        
        .badges-container {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin: 20px 0;
        }
        
        .badge {
            width: 70px;
            height: 70px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            background: linear-gradient(135deg, #ffba08 0%, #faa307 100%);
            color: white;
            font-size: 1.8rem;
            position: relative;
            border: 3px solid white;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
            transition: all 0.3s ease;
        }
        
        .badge.locked {
            background: linear-gradient(135deg, #6c757d 0%, #495057 100%);
            color: #adb5bd;
        }
        
        .badge-info {
            position: absolute;
            bottom: -30px;
            left: 50%;
            transform: translateX(-50%);
            background: rgba(0, 0, 0, 0.8);
            padding: 5px 10px;
            border-radius: 5px;
            font-size: 0.8rem;
            white-space: nowrap;
            opacity: 0;
            transition: opacity 0.3s ease;
        }
        
        .badge:hover .badge-info {
            opacity: 1;
        }
        
        .help-button {
            position: absolute;
            top: 15px;
            right: 15px;
            width: 30px;
            height: 30px;
            border-radius: 50%;
            background: var(--primary);
            color: white;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            font-weight: bold;
        }
        
        .grammar-help {
            position: absolute;
            top: 50px;
            right: 0;
            width: 300px;
            background: rgba(255, 255, 255, 0.95);
            color: var(--dark);
            border-radius: 10px;
            padding: 15px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
            z-index: 100;
            display: none;
        }
        
        .grammar-help h3 {
            color: var(--primary);
            margin-bottom: 10px;
        }
        
        .grammar-help p {
            margin-bottom: 10px;
            line-height: 1.4;
        }
        
        .grammar-help .example {
            background: #f8f9fa;
            padding: 10px;
            border-radius: 5px;
            font-style: italic;
            margin: 10px 0;
            border-left: 3px solid var(--primary);
        }
        
        .close-help {
            position: absolute;
            top: 5px;
            right: 10px;
            cursor: pointer;
            font-weight: bold;
            color: var(--dark);
        }
        
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        
        @keyframes slideIn {
            from { transform: translateX(-20px); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }
        
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
        
        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% {transform: translateY(0);}
            40% {transform: translateY(-20px);}
            60% {transform: translateY(-10px);}
        }
        
        .badge.unlocked {
            animation: bounce 1s;
        }
        
        @media (max-width: 768px) {
            .game-container {
                grid-template-columns: 1fr;
            }
            
            .options-container {
                grid-template-columns: 1fr;
            }
            
            input, select {
                width: 100%;
            }
            
            .grammar-help {
                width: 90%;
                left: 5%;
                right: 5%;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>Grammar Quest Champions</h1>
            <p class="subtitle">Desafía tus conocimientos de gramática inglesa en competencia con otros jugadores</p>
        </header>

        <!-- Pantalla de Lobby -->
        <div id="lobby" class="game-screen">
            <h2 class="screen-title">Sala de Espera</h2>
            
            <div class="player-form">
                <input type="text" id="playerName" placeholder="Ingresa tu nombre" maxlength="15">
                
                <h3>Selecciona tu avatar:</h3>
                <div class="avatar-selection" id="avatarSelection">
                    <div class="avatar-option" data-avatar="👨‍💻" style="background: #4cc9f0;">👨‍💻</div>
                    <div class="avatar-option" data-avatar="👩‍🎓" style="background: #f72585;">👩‍🎓</div>
                    <div class="avatar-option" data-avatar="🧙‍♂️" style="background: #7209b7;">🧙‍♂️</div>
                    <div class="avatar-option" data-avatar="👨‍🚀" style="background: #3a0ca3;">👨‍🚀</div>
                    <div class="avatar-option" data-avatar="👸" style="background: #ffba08;">👸</div>
                </div>
                
                <button onclick="joinGame()">Unirse al juego</button>
            </div>
            
            <h3 class="screen-title">Jugadores conectados: <span id="playersCount">0</span>/4</h3>
            
            <div class="players-container" id="playersList">
                <!-- Jugadores aparecerán aquí -->
            </div>
            
            <div class="player-form">
                <button id="startGameBtn" onclick="startGame()" disabled>Iniciar juego</button>
            </div>
        </div>

        <!-- Pantalla de Juego -->
        <div id="game" class="game-screen">
            <div class="level-indicator">
                Nivel: <span id="currentLevel">1</span> de 5
            </div>
            
            <div class="progress-bar">
                <div class="progress" id="levelProgress" style="width: 0%"></div>
            </div>
            
            <div class="badges-container" id="badgesContainer">
                <!-- Insignias aparecerán aquí -->
            </div>
            
            <div class="game-container">
                <div class="left-panel">
                    <div class="question-box">
                        <div class="help-button" id="helpButton">?</div>
                        <div class="grammar-help" id="grammarHelp">
                            <div class="close-help" id="closeHelp">X</div>
                            <h3 id="helpTitle">Título de ayuda</h3>
                            <p id="helpContent">Contenido de ayuda gramatical...</p>
                            <div class="example" id="helpExample"></div>
                        </div>
                        
                        <div class="question-text" id="questionText">
                            <!-- Pregunta aparecerá aquí -->
                        </div>
                        
                        <div class="options-container" id="optionsContainer">
                            <!-- Opciones aparecerán aquí -->
                        </div>
                    </div>
                    
                    <div class="timer-container">
                        <div class="timer" id="timer">30</div>
                        <p>segundos restantes</p>
                    </div>
                </div>
                
                <div class="score-board">
                    <h3 class="score-title">Puntuación</h3>
                    <div id="scores">
                        <!-- Puntuaciones aparecerán aquí -->
                    </div>
                </div>
            </div>
        </div>

        <!-- Pantalla de Resultados -->
        <div id="results" class="game-screen">
            <h2 class="screen-title">Resultados Finales</h2>
            
            <div class="results-container">
                <div class="winner-badge" id="winnerText"></div>
                
                <div class="badges-container" id="finalBadges">
                    <!-- Insignias finales aparecerán aquí -->
                </div>
                
                <div id="finalResults">
                    <!-- Resultados aparecerán aquí -->
                </div>
                
                <button onclick="resetGame()">Jugar de nuevo</button>
            </div>
        </div>
    </div>

    <script>
        // Variables globales
        let players = {};
        let currentPlayerId = null;
        let currentQuestion = null;
        let timeLeft = 30;
        let timerInterval = null;
        let currentLevel = 1;
        let questionsAnswered = 0;
        const QUESTIONS_PER_LEVEL = 5;
        let playerAvatar = "👨‍💻";
        let badgesEarned = [];
        
        // Información de ayuda gramatical
        const grammarHelp = {
            "present_simple": {
                title: "Present Simple",
                content: "El Present Simple se utiliza para expresar rutinas, hábitos, hechos generales y situaciones permanentes.",
                example: "She works at a bank. (Ella trabaja en un banco).\nI play tennis every Tuesday. (Juego tenis todos los martes)."
            },
            "present_continuous": {
                title: "Present Continuous",
                content: "El Present Continuous se utiliza para describir acciones que están ocurriendo en el momento actual o planes futuros.",
                example: "I am studying for my exam. (Estoy estudiando para mi examen).\nThey are visiting us next week. (Ellos nos visitan la próxima semana)."
            },
            "plurals": {
                title: "Plural Nouns",
                content: "La mayoría de sustantivos forman el plural añadiendo -s. Pero hay excepciones: palabras que terminan en -ch, -sh, -s, -x, -z añaden -es. Palabras que terminan en consonante + y cambian la y por i y añaden -es.",
                example: "child → children (niño → niños)\nwoman → women (mujer → mujeres)"
            },
            "possessives": {
                title: "Possessive Forms",
                content: "Para mostrar posesión en inglés, se usa 's para personas y animales, y of para cosas. Para sustantivos plurales que terminan en s, solo se añade el apóstrofo.",
                example: "John's car (el coche de John)\nThe students' books (los libros de los estudiantes)"
            },
            "articles": {
                title: "Articles (a, an, the)",
                content: "Se usa 'a' antes de sonidos de consonante, 'an' antes de sonidos de vocal. 'The' se usa para cosas específicas o ya mencionadas.",
                example: "a university (una universidad)\nan hour (una hora)\nthe book I told you about (el libro del que te hablé)"
            },
            "past_perfect": {
                title: "Past Perfect",
                content: "El Past Perfect se utiliza para describir una acción que ocurrió antes de otra acción en el pasado. Se forma con had + participio pasado.",
                example: "When we arrived, they had already left. (Cuando llegamos, ellos ya se habían ido)."
            },
            "conditionals": {
                title: "Conditionals",
                content: "El primer condicional se usa para situaciones reales o probables: If + present simple, will + infinitive.",
                example: "If it rains, we will cancel the picnic. (Si llueve, cancelaremos el picnic)."
            },
            "comparatives": {
                title: "Comparative Adjectives",
                content: "Los adjetivos cortos (1-2 sílabas) añaden -er. Los adjetivos largos usan 'more' antes del adjetivo. Algunos adjetivos son irregulares.",
                example: "big → bigger (grande → más grande)\nbeautiful → more beautiful (hermoso → más hermoso)"
            },
            "tag_questions": {
                title: "Tag Questions",
                content: "Las tag questions se forman con el auxiliar contrario al de la frase principal. Si la frase es afirmativa, la tag es negativa y viceversa.",
                example: "She's coming, isn't she? (Ella viene, ¿no?)\nYou don't like coffee, do you? (No te gusta el café, ¿verdad?)"
            },
            "prepositions": {
                title: "Prepositions",
                content: "Las preposiciones expresan relaciones entre palabras. 'At' para puntos específicos, 'in' para espacios cerrados, 'on' para superficies.",
                example: "good at math (bueno en matemáticas)\ninterested in music (interesado en música)"
            }
        };
        
        // Configuración de insignias por nivel
        const levelBadges = {
            1: { 
                name: "Grammar Novice", 
                icon: "📚", 
                pointsRequired: 1000,
                description: "Completa el Nivel 1 con al menos 1000 puntos"
            },
            2: { 
                name: "Language Learner", 
                icon: "🎯", 
                pointsRequired: 2500,
                description: "Completa el Nivel 2 con al menos 2500 puntos"
            },
            3: { 
                name: "Syntax Specialist", 
                icon: "⭐", 
                pointsRequired: 4500,
                description: "Completa el Nivel 3 con al menos 4500 puntos"
            },
            4: { 
                name: "Grammar Guru", 
                icon: "🏆", 
                pointsRequired: 7000,
                description: "Completa el Nivel 4 con al menos 7000 puntos"
            },
            5: { 
                name: "Master Linguist", 
                icon: "👑", 
                pointsRequired: 10000,
                description: "Completa el Nivel 5 con al menos 10000 puntos"
            }
        };

        // Preguntas por nivel de dificultad
        let questions = {
            1: [
                {
                    question: "Choose the correct present simple form: She ___ to school every day.",
                    options: ["go", "goes", "going", "went"],
                    correct: 1,
                    helpKey: "present_simple"
                },
                {
                    question: "Which sentence is in present continuous?",
                    options: ["I eat breakfast", "I eating breakfast", "I am eating breakfast", "I eaten breakfast"],
                    correct: 2,
                    helpKey: "present_continuous"
                },
                {
                    question: "Select the correct plural form: one child, two ___",
                    options: ["childs", "children", "childes", "child"],
                    correct: 1,
                    helpKey: "plurals"
                },
                {
                    question: "Which is a correct possessive form?",
                    options: ["Johns book", "John's book", "Johns' book", "John book"],
                    correct: 1,
                    helpKey: "possessives"
                },
                {
                    question: "Choose the correct article: ___ apple a day keeps the doctor away.",
                    options: ["A", "An", "The", "No article"],
                    correct: 1,
                    helpKey: "articles"
                }
            ],
            2: [
                {
                    question: "Select the correct past perfect form: They ___ already ___ when we arrived.",
                    options: ["had, left", "have, left", "were, leaving", "did, leave"],
                    correct: 0,
                    helpKey: "past_perfect"
                },
                {
                    question: "Which sentence uses the first conditional correctly?",
                    options: ["If it will rain, we will cancel the picnic.", "If it rains, we will cancel the picnic.", "If it rain, we will cancel the picnic.", "If it rained, we will cancel the picnic."],
                    correct: 1,
                    helpKey: "conditionals"
                },
                {
                    question: "Choose the correct comparative form: This book is ___ than the movie.",
                    options: ["interesting", "more interesting", "most interesting", "interestinger"],
                    correct: 1,
                    helpKey: "comparatives"
                },
                {
                    question: "Identify the correct tag question: She's coming to the party, ___?",
                    options: ["is she", "isn't she", "does she", "doesn't she"],
                    correct: 1,
                    helpKey: "tag_questions"
                },
                {
                    question: "Select the correct preposition: I'm good ___ math.",
                    options: ["at", "in", "on", "with"],
                    correct: 0,
                    helpKey: "prepositions"
                }
            ],
            3: [
                {
                    question: "Which sentence uses the passive voice correctly?",
                    options: ["The cake was eaten by the children.", "The cake eaten by the children.", "The cake is eat by the children.", "The cake was ate by the children."],
                    correct: 0,
                    helpKey: "passive_voice"
                },
                {
                    question: "Choose the correct reported speech: 'I will help you,' she said.",
                    options: ["She said that she will help me.", "She said that she would help me.", "She said that she helps me.", "She said that she would helped me."],
                    correct: 1,
                    helpKey: "reported_speech"
                },
                {
                    question: "Identify the correct relative pronoun: The person ___ called you is my boss.",
                    options: ["which", "who", "whom", "whose"],
                    correct: 1,
                    helpKey: "relative_pronouns"
                },
                {
                    question: "Select the correct modal verb: You ___ finish your homework before going out.",
                    options: ["must", "can", "may", "would"],
                    correct: 0,
                    helpKey: "modal_verbs"
                },
                {
                    question: "Which is an example of the second conditional?",
                    options: ["If I win the lottery, I will buy a car.", "If I won the lottery, I would buy a car.", "If I had won the lottery, I would have bought a car.", "If I win the lottery, I would buy a car."],
                    correct: 1,
                    helpKey: "conditionals"
                }
            ],
            4: [
                {
                    question: "Choose the correct participle phrase: ___, the book was fascinating.",
                    options: ["Written in 1920", "Writing in 1920", "Wrote in 1920", "Write in 1920"],
                    correct: 0,
                    helpKey: "participle_phrases"
                },
                {
                    question: "Identify the sentence with correct inversion:",
                    options: ["Never I have seen such a beautiful sunset.", "Never have I seen such a beautiful sunset.", "Never I have seen such a beautiful sunset.", "I never have seen such a beautiful sunset."],
                    correct: 1,
                    helpKey: "inversion"
                },
                {
                    question: "Select the correct subjunctive form: It's essential that he ___ on time.",
                    options: ["arrive", "arrives", "arrived", "will arrive"],
                    correct: 0,
                    helpKey: "subjunctive"
                },
                {
                    question: "Which sentence contains a dangling modifier?",
                    options: ["Running quickly, the bus was caught by the man.", "The man caught the bus while running quickly.", "Running quickly, the man caught the bus.", "The bus was caught by the man running quickly."],
                    correct: 0,
                    helpKey: "dangling_modifiers"
                },
                {
                    question: "Choose the correct conditional: If I ___ earlier, I wouldn't have missed the train.",
                    options: ["had left", "left", "would leave", "have left"],
                    correct: 0,
                    helpKey: "conditionals"
                }
            ],
            5: [
                {
                    question: "Identify the correct mixed conditional:",
                    options: ["If I had studied medicine, I would be a doctor now.", "If I studied medicine, I would be a doctor now.", "If I had studied medicine, I would have been a doctor now.", "If I study medicine, I would be a doctor now."],
                    correct: 0,
                    helpKey: "conditionals"
                },
                {
                    question: "Select the sentence with correct use of 'lest':",
                    options: ["He studied hard lest he should fail the exam.", "He studied hard lest he fails the exam.", "He studied hard lest he failed the exam.", "He studied hard lest he would fail the exam."],
                    correct: 0,
                    helpKey: "conjunctions"
                },
                {
                    question: "Choose the correct emphatic structure: ___ was the music that I couldn't concentrate.",
                    options: ["Such", "So", "Very", "Too"],
                    correct: 0,
                    helpKey: "emphatic_structures"
                },
                {
                    question: "Identify the correct use of 'were' subjunctive:",
                    options: ["I wish I were more organized.", "I wish I was more organized.", "I wish I am more organized.", "I wish I will be more organized."],
                    correct: 0,
                    helpKey: "subjunctive"
                },
                {
                    question: "Select the correct participle clause: ___, she didn't notice the time.",
                    options: ["Absorbed in her work", "Absorbing in her work", "Being absorbed in her work", "Having absorbed in her work"],
                    correct: 0,
                    helpKey: "participle_clauses"
                }
            ]
        };

        // Inicializar el juego
        function init() {
            setupAvatarSelection();
            setupGrammarHelp();
            generateBadgesDisplay();
        }
        
        // Configurar selección de avatar
        function setupAvatarSelection() {
            const avatarOptions = document.querySelectorAll('.avatar-option');
            avatarOptions.forEach(option => {
                option.addEventListener('click', () => {
                    avatarOptions.forEach(opt => opt.classList.remove('selected'));
                    option.classList.add('selected');
                    playerAvatar = option.getAttribute('data-avatar');
                });
            });
        }
        
        // Configurar sistema de ayuda gramatical
        function setupGrammarHelp() {
            const helpButton = document.getElementById('helpButton');
            const grammarHelp = document.getElementById('grammarHelp');
            const closeHelp = document.getElementById('closeHelp');
            
            helpButton.addEventListener('click', () => {
                grammarHelp.style.display = 'block';
            });
            
            closeHelp.addEventListener('click', () => {
                grammarHelp.style.display = 'none';
            });
        }
        
        // Generar display de insignias
        function generateBadgesDisplay() {
            const badgesContainer = document.getElementById('badgesContainer');
            badgesContainer.innerHTML = '';
            
            for (let level = 1; level <= 5; level++) {
                const badge = document.createElement('div');
                badge.className = 'badge locked';
                badge.innerHTML = `
                    ${levelBadges[level].icon}
                    <div class="badge-info">${levelBadges[level].description}</div>
                `;
                badge.id = `badge-level-${level}`;
                badgesContainer.appendChild(badge);
            }
        }

        // Función para unirse al juego
        function joinGame() {
            const playerName = document.getElementById('playerName').value.trim();
            if (!playerName) return alert('Por favor ingresa tu nombre');
            
            // Simular conexión (en realidad sería con un servidor)
            currentPlayerId = 'player_' + Date.now();
            players[currentPlayerId] = {
                id: currentPlayerId,
                name: playerName,
                score: 0,
                level: 1,
                avatar: playerAvatar,
                badges: []
            };
            
            updatePlayersList();
            document.getElementById('startGameBtn').disabled = false;
            document.getElementById('playerName').disabled = true;
            
            // Simular otros jugadores (en un juego real vendrían del servidor)
            simulateOtherPlayers();
        }
        
        // Simular otros jugadores (solo para demostración)
        function simulateOtherPlayers() {
            const demoPlayers = [
                {name: "Ana", avatar: "👩‍🎓"},
                {name: "Luis", avatar: "🧙‍♂️"},
                {name: "Marta", avatar: "👸"}
            ];
            
            demoPlayers.forEach((player, index) => {
                setTimeout(() => {
                    const id = 'demo_' + index;
                    players[id] = {
                        id: id,
                        name: player.name,
                        score: 0,
                        level: 1,
                        avatar: player.avatar,
                        isDemo: true,
                        badges: []
                    };
                    updatePlayersList();
                }, 1000 * (index + 1));
            });
        }

        // Actualizar lista de jugadores
        function updatePlayersList() {
            const playersList = document.getElementById('playersList');
            const playersCount = document.getElementById('playersCount');
            
            playersList.innerHTML = '';
            playersCount.textContent = Object.keys(players).length;
            
            for (const id in players) {
                const player = players[id];
                const playerCard = document.createElement('div');
                playerCard.className = 'player-card';
                playerCard.innerHTML = `
                    <div class="player-avatar" style="background: ${getAvatarColor(player.avatar)};">${player.avatar}</div>
                    <div class="player-name">${player.name}</div>
                `;
                playersList.appendChild(playerCard);
            }
        }
        
        // Obtener color basado en avatar
        function getAvatarColor(avatar) {
            const colors = {
                "👨‍💻": "#4cc9f0",
                "👩‍🎓": "#f72585",
                "🧙‍♂️": "#7209b7",
                "👨‍🚀": "#3a0ca3",
                "👸": "#ffba08"
            };
            return colors[avatar] || "#4361ee";
        }

        // Iniciar el juego
        function startGame() {
            document.getElementById('lobby').style.display = 'none';
            document.getElementById('game').style.display = 'block';
            
            // Iniciar el primer nivel
            loadLevel(currentLevel);
            updateScores();
        }

        // Cargar nivel
        function loadLevel(level) {
            document.getElementById('currentLevel').textContent = level;
            resetProgressBar();
            showQuestion(questions[level][0]);
        }
        
        // Reiniciar barra de progreso
        function resetProgressBar() {
            questionsAnswered = 0;
            updateProgressBar();
        }
        
        // Actualizar barra de progreso
        function updateProgressBar() {
            const progress = (questionsAnswered / QUESTIONS_PER_LEVEL) * 100;
            document.getElementById('levelProgress').style.width = `${progress}%`;
        }

        // Mostrar pregunta
        function showQuestion(question) {
            currentQuestion = question;
            document.getElementById('questionText').textContent = question.question;
            
            // Actualizar ayuda gramatical
            if (question.helpKey && grammarHelp[question.helpKey]) {
                const help = grammarHelp[question.helpKey];
                document.getElementById('helpTitle').textContent = help.title;
                document.getElementById('helpContent').textContent = help.content;
                document.getElementById('helpExample').textContent = help.example;
            }
            
            const optionsContainer = document.getElementById('optionsContainer');
            optionsContainer.innerHTML = '';
            
            question.options.forEach((option, index) => {
                const button = document.createElement('button');
                button.className = 'option-btn';
                button.textContent = option;
                button.onclick = () => checkAnswer(index);
                optionsContainer.appendChild(button);
            });
            
            // Iniciar temporizador
            startTimer();
        }
        
        // Iniciar temporizador
        function startTimer() {
            timeLeft = 30;
            document.getElementById('timer').textContent = timeLeft;
            
            if (timerInterval) clearInterval(timerInterval);
            timerInterval = setInterval(updateTimer, 1000);
        }

        // Actualizar temporizador
        function updateTimer() {
            timeLeft--;
            document.getElementById('timer').textContent = timeLeft;
            
            if (timeLeft <= 0) {
                clearInterval(timerInterval);
                // Pasar a la siguiente pregunta
                nextQuestion();
            }
        }

        // Verificar respuesta
        function checkAnswer(selectedIndex) {
            clearInterval(timerInterval);
            
            const isCorrect = selectedIndex === currentQuestion.correct;
            if (isCorrect) {
                // Calcular puntos basados en el tiempo restante
                const pointsEarned = timeLeft * 10;
                players[currentPlayerId].score += pointsEarned;
                
                // Dar puntos también a jugadores demo (aleatoriamente)
                for (const id in players) {
                    if (players[id].isDemo) {
                        // Los jugadores demo responden correctamente el 70% del tiempo
                        if (Math.random() > 0.3) {
                            players[id].score += Math.floor(timeLeft * 10 * Math.random());
                        }
                    }
                }
                
                updateScores();
            }
            
            // Pausa breve antes de continuar
            setTimeout(nextQuestion, 1500);
        }
        
        // Siguiente pregunta
        function nextQuestion() {
            questionsAnswered++;
            updateProgressBar();
            
            if (questionsAnswered < QUESTIONS_PER_LEVEL) {
                // Mostrar siguiente pregunta del mismo nivel
                showQuestion(questions[currentLevel][questionsAnswered]);
            } else if (currentLevel < 5) {
                // Verificar si se ganó una insignia por este nivel
                checkForBadge();
                
                // Avanzar al siguiente nivel
                currentLevel++;
                loadLevel(currentLevel);
            } else {
                // Verificar si se ganó una insignia por el último nivel
                checkForBadge();
                
                // Finalizar juego
                endGame();
            }
        }
        
        // Verificar si el jugador ganó una insignia
        function checkForBadge() {
            const player = players[currentPlayerId];
            const badgeInfo = levelBadges[currentLevel];
            
            if (player.score >= badgeInfo.pointsRequired && !player.badges.includes(currentLevel)) {
                player.badges.push(currentLevel);
                badgesEarned.push(currentLevel);
                
                // Mostrar insignia desbloqueada
                const badgeElement = document.getElementById(`badge-level-${currentLevel}`);
                badgeElement.classList.remove('locked');
                badgeElement.classList.add('unlocked');
                
                // Animación
                setTimeout(() => {
                    badgeElement.classList.remove('unlocked');
                }, 1000);
            }
        }

        // Actualizar tabla de puntuaciones
        function updateScores() {
            const scoresContainer = document.getElementById('scores');
            scoresContainer.innerHTML = '';
            
            // Ordenar jugadores por puntuación
            const sortedPlayers = Object.values(players).sort((a, b) => b.score - a.score);
            
            sortedPlayers.forEach((player, index) => {
                const scoreItem = document.createElement('div');
                scoreItem.className = 'score-item';
                if (player.id === currentPlayerId) {
                    scoreItem.classList.add('highlight');
                }
                
                scoreItem.innerHTML = `
                    <span>${index + 1}. ${player.name}</span>
                    <span>${player.score} pts</span>
                `;
                
                scoresContainer.appendChild(scoreItem);
            });
        }

        // Finalizar juego
        function endGame() {
            document.getElementById('game').style.display = 'none';
            document.getElementById('results').style.display = 'block';
            
            const finalResults = document.getElementById('finalResults');
            finalResults.innerHTML = '';
            
            // Mostrar insignias ganadas
            showFinalBadges();
            
            // Ordenar jugadores por puntuación
            const sortedPlayers = Object.values(players).sort((a, b) => b.score - a.score);
            const winner = sortedPlayers[0];
            
            document.getElementById('winnerText').textContent = `¡${winner.name} es el ganador!`;
            
            sortedPlayers.forEach((player, index) => {
                const resultItem = document.createElement('div');
                resultItem.className = 'score-item';
                if (player.id === currentPlayerId) {
                    resultItem.classList.add('highlight');
                }
                
                resultItem.innerHTML = `
                    <span>${index + 1}. ${player.name}</span>
                    <span>${player.score} puntos</span>
                `;
                
                finalResults.appendChild(resultItem);
            });
        }
        
        // Mostrar insignias finales
        function showFinalBadges() {
            const finalBadgesContainer = document.getElementById('finalBadges');
            finalBadgesContainer.innerHTML = '<h3>Insignias obtenidas:</h3>';
            
            const badgesContainer = document.createElement('div');
            badgesContainer.className = 'badges-container';
            
            for (let level = 1; level <= 5; level++) {
                const badge = document.createElement('div');
                
                if (badgesEarned.includes(level)) {
                    badge.className = 'badge';
                    badge.innerHTML = levelBadges[level].icon;
                } else {
                    badge.className = 'badge locked';
                    badge.innerHTML = levelBadges[level].icon;
                }
                
                badgesContainer.appendChild(badge);
            }
            
            finalBadgesContainer.appendChild(badgesContainer);
        }
        
        // Reiniciar juego
        function resetGame() {
            document.getElementById('results').style.display = 'none';
            document.getElementById('lobby').style.display = 'block';
            
            // Reiniciar variables
            players = {};
            currentPlayerId = null;
            currentLevel = 1;
            badgesEarned = [];
            
            // Habilitar entrada de nombre
            document.getElementById('playerName').disabled = false;
            document.getElementById('playerName').value = '';
            document.getElementById('startGameBtn').disabled = true;
            
            // Limpiar lista de jugadores
            document.getElementById('playersList').innerHTML = '';
            document.getElementById('playersCount').textContent = '0';
            
            // Regenerar insignias
            generateBadgesDisplay();
        }
        
        // Inicializar el juego cuando se carga la página
        window.onload = init;
    </script>
</body>
</html>
