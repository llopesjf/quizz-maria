<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quizz para a Maria</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #e6f2ff;
            text-align: center;
            padding: 20px;
            color: #1a5276;
        }
        .page {
            max-width: 600px;
            margin: 0 auto;
            background-color: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            display: none;
        }
        .active {
            display: block;
        }
        h1 {
            color: #2874a6;
        }
        .question {
            margin: 20px 0;
            font-weight: bold;
            font-size: 1.2em;
            color: #1a5276;
            position: relative;
        }
        .question.correct::after {
            content: "✓";
            color: #2ecc71;
            font-size: 1.5em;
            position: absolute;
            right: -30px;
            top: 50%;
            transform: translateY(-50%);
        }
        .question.wrong::after {
            content: "✗";
            color: #e74c3c;
            font-size: 1.5em;
            position: absolute;
            right: -30px;
            top: 50%;
            transform: translateY(-50%);
        }
        .options {
            display: flex;
            flex-direction: column;
            gap: 16px;
            margin: 20px 0;
        }
        .option-row {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        button.option {
            background-color: white;
            color: #2874a6;
            border: 2px solid #2874a6;
            padding: 10px 10px;
            border-radius: 5px;
            cursor: pointer;
            transition: all 0.3s;
            text-align: left;
            position: relative;
            flex: 1 1 auto;
            font-size: 1em;
        }
        button.option:hover {
            background-color: #d4e6f1;
        }
        button.option.selected {
            background-color: #3498db;
            color: white;
            border-color: #3498db;
            box-shadow: 0 0 10px rgba(52, 152, 219, 0.5);
        }
        button.option.correct {
            background-color: #2ecc71;
            color: white;
            border-color: #27ae60;
        }
        button.option.correct::after {
            content: "✓";
            position: absolute;
            right: 15px;
        }
        button.option.wrong {
            background-color: #e74c3c;
            color: white;
            border-color: #c0392b;
        }
        button.option.wrong::after {
            content: "✗";
            position: absolute;
            right: 15px;
        }
        .player-btn {
            background: #2874a6;
            color: #fff;
            border: none;
            border-radius: 50%;
            width: 36px;
            height: 36px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.2em;
            cursor: pointer;
            transition: background 0.2s, transform 0.2s;
        }
        .player-btn:active,
        .player-btn.playing {
            background: #2ecc71;
            transform: scale(1.1);
        }
        .music-embed {
            display: none;
        }
        #result {
            font-size: 1.2em;
            margin: 20px 0;
            color: #1a5276;
        }
        #restart-btn {
            background-color: #e74c3c;
            margin: 20px auto;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            color: white;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        #restart-btn:hover {
            background-color: #c0392b;
        }
        .progress-container {
            width: 100%;
            background-color: #f1f1f1;
            border-radius: 5px;
            margin: 20px 0;
        }
        .progress-bar {
            height: 10px;
            background-color: #2874a6;
            border-radius: 5px;
            width: 0%;
            transition: width 0.5s;
        }
        #video-container {
            position: relative;
            width: 100%;
            max-width: 500px;
            margin: 20px auto;
            background: #000;
            border-radius: 10px;
            overflow: hidden;
        }
        .iframe-video {
            width: 100%;
            height: 315px;
            border: none;
            border-radius: 10px;
            background: #000;
        }
        .video-action-btn {
            background-color: #2874a6;
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 30px;
            font-size: 1em;
            cursor: pointer;
            margin-top: 15px;
            transition: all 0.3s;
        }
        .video-action-btn:hover {
            background-color: #1a5276;
            transform: scale(1.05);
        }
        #video-fallback {
            display: none;
            padding: 20px;
            color: white;
        }
        .heart {
            color: #e74c3c;
            font-size: 1.5em;
            animation: pulse 1.5s infinite;
        }
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.3); }
            100% { transform: scale(1); }
        }
    </style>
</head>
<body>
    <div class="progress-container">
        <div class="progress-bar" id="progressBar"></div>
    </div>

    <!-- Página 1: Pergunta 1 -->
    <div class="page active" id="page1">
        <h1>Quizz para a Maria ❤️</h1>
        <div class="question" id="question1">1. Música que mais me faz lembrar você:</div>
        <div class="options">
            <div class="option-row">
                <button class="option" onclick="selectOption(this, 1, 'Opção Errada')">Química (Little Hair)</button>
                <button class="player-btn" onclick="playSoundcloud(this, 'https://w.soundcloud.com/player/?url=https%3A//soundcloud.com/eriickballa/mc-cabelinho-quimica-prod-pep-starling&color=%232874a6&inverse=false&auto_play=true&show_user=true')" type="button" title="Tocar música">
                    ▶
                </button>
            </div>
            <div class="option-row">
                <button class="option" onclick="selectOption(this, 1, 'Te encontrar (Modéstia parte)')">Te encontrar (Modéstia parte)</button>
                <button class="player-btn" onclick="playSoundcloud(this, 'https://w.soundcloud.com/player/?url=https%3A//soundcloud.com/modestiaparteofficial/te-encontrar&color=%232874a6&inverse=false&auto_play=true&show_user=true')" type="button" title="Tocar música">
                    ▶
                </button>
            </div>
            <div class="option-row">
                <button class="option" onclick="selectOption(this, 1, 'Opção Errada')">Duro Igual Concreto (1Kilo)</button>
                <button class="player-btn" onclick="playSoundcloud(this, 'https://w.soundcloud.com/player/?url=https%3A//soundcloud.com/dj-kb-do-ytb/1-kilo-duro-igual-concreto&color=%232874a6&inverse=false&auto_play=true&show_user=true')" type="button" title="Tocar música">
                    ▶
                </button>
            </div>
            <div class="option-row">
                <button class="option" onclick="selectOption(this, 1, 'Opção Errada')">Bandido não, Malandro! (2ZDinizz)</button>
                <button class="player-btn" onclick="playSoundcloud(this, 'https://w.soundcloud.com/player/?url=https%3A//soundcloud.com/2zdinizz-music/bandido-nao-malandro&color=%232874a6&inverse=false&auto_play=true&show_user=true')" type="button" title="Tocar música">
                    ▶
                </button>
            </div>
        </div>
        <div id="sc-modal" style="display:none; position:fixed; top:0;left:0;right:0;bottom:0; background:rgba(40,116,166,0.92); z-index:9999; align-items:center; justify-content:center;">
            <div style="max-width:400px;width:90%;margin:40px auto;background:#fff;border-radius:12px;box-shadow:0 0 30px #0008;padding:18px 12px 12px 12px;position:relative;">
                <button onclick="closeModal()" style="position:absolute;top:8px;right:12px;font-size:1.5em;background:none;border:none;color:#2874a6;cursor:pointer;">×</button>
                <iframe id="sc-iframe" width="100%" height="120" scrolling="no" frameborder="no" allow="autoplay"></iframe>
            </div>
        </div>
    </div>

    <!-- Página 2: Pergunta 2 -->
    <div class="page" id="page2">
        <h1>Quizz para a Maria ❤️</h1>
        <div class="question" id="question2">2. Quando olho nos seus olhos, o que vem na minha cabeça?</div>
        <div class="options">
            <button class="option" onclick="selectOption(this, 2, 'Opção Errada')">Mar</button>
            <button class="option" onclick="selectOption(this, 2, 'Opção Errada')">Sol</button>
            <button class="option" onclick="selectOption(this, 2, 'Estrelas')">Estrelas</button>
            <button class="option" onclick="selectOption(this, 2, 'Opção Errada')">Lua Cheia</button>
        </div>
    </div>

    <!-- Página 3: Pergunta 3 -->
    <div class="page" id="page3">
        <h1>Quizz para a Maria ❤️</h1>
        <div class="question" id="question3">3. Qual vai ser o nome do nosso cachorro?</div>
        <div class="options">
            <button class="option" onclick="selectOption(this, 3, 'Opção Errada')">Luna</button>
            <button class="option" onclick="selectOption(this, 3, 'Kush')">Kush</button>
            <button class="option" onclick="selectOption(this, 3, 'Opção Errada')">Rex</button>
            <button class="option" onclick="selectOption(this, 3, 'Opção Errada')">Bob</button>
        </div>
    </div>

    <!-- Página 4: Pergunta 4 -->
    <div class="page" id="page4">
        <h1>Quizz para a Maria ❤️</h1>
        <div class="question" id="question4">4. Qual nosso destino?</div>
        <div class="options">
            <button class="option" onclick="selectOption(this, 4, 'Opção Errada')">Itália</button>
            <button class="option" onclick="selectOption(this, 4, 'Opção Errada')">Brasil</button>
            <button class="option" onclick="selectOption(this, 4, 'Portugal')">Portugal</button>
            <button class="option" onclick="selectOption(this, 4, 'Opção Errada')">Espanha</button>
        </div>
    </div>

    <!-- Página 5: Pergunta 5 - Nosso primeiro beijo -->
    <div class="page" id="page5">
        <h1>Quizz para a Maria ❤️</h1>
        <div class="question" id="question5">5. Quando foi nosso primeiro beijo?</div>
        <div class="options">
            <button class="option" onclick="selectOption(this, 5, 'Opção Errada')">30/06/2025</button>
            <button class="option" onclick="selectOption(this, 5, 'Opção Errada')">22/05/2025</button>
            <button class="option" onclick="selectOption(this, 5, '09/04/2025')">09/04/2025</button>
            <button class="option" onclick="selectOption(this, 5, 'Opção Errada')">15/03/2025</button>
        </div>
    </div>

    <!-- Página Final: Vídeo Surpresa -->
    <div class="page" id="page6">
        <h1>Para você, meu amor <span class="heart">❤️</span></h1>
        <div id="result"></div>
        <div id="video-container">
            <iframe 
                class="iframe-video"
                src="https://drive.google.com/file/d/1Py35d1ZAaV1P-mKLFAuP0z87tzOpD8BH/preview"
                allow="autoplay"
                allowfullscreen
            ></iframe>
            <div id="video-fallback" style="display:none;">
                <p>Não foi possível carregar o vídeo automaticamente.</p>
                <a href="https://drive.google.com/file/d/1Py35d1ZAaV1P-mKLFAuP0z87tzOpD8BH/view?usp=drive_link" class="video-action-btn" target="_blank">
                    Clique para ver nosso vídeo especial
                </a>
            </div>
        </div>
        <p>Esse momento merecia ser eternizado! Espero não virar meme!</p>
    </div>

    <!-- Página de Reinício -->
    <div class="page" id="page7">
        <h1>Quizz para a Maria ❤️</h1>
        <div id="result-fail">
            <p>Você acertou <span id="score">0</span> de 5 perguntas.</p>
            <p>Precisamos nos conhecer melhor!</p>
        </div>
        <button id="restart-btn" onclick="restartQuiz()">Refazer Quizz</button>
    </div>

    <script>
        let currentPage = 1;
        const totalPages = 7;
        let answers = {
            1: null,
            2: null,
            3: null,
            4: null,
            5: null
        };
        const correctAnswers = {
            1: "Te encontrar (Modéstia parte)",
            2: "Estrelas",
            3: "Kush",
            4: "Portugal",
            5: "09/04/2025"
        };

        function updateProgress() {
            const progress = ((currentPage - 1) / (totalPages - 2)) * 100;
            document.getElementById('progressBar').style.width = progress + '%';
        }

        function selectOption(element, question, answer) {
            const options = document.querySelectorAll(`#page${question} .option`);
            options.forEach(option => {
                option.classList.remove('selected', 'correct', 'wrong');
                option.disabled = true;
            });
            element.classList.add('selected');
            answers[question] = answer;
            if (answer === correctAnswers[question]) {
                element.classList.add('correct');
                document.getElementById(`question${question}`).classList.add('correct');
                document.getElementById(`question${question}`).classList.remove('wrong');
            } else {
                element.classList.add('wrong');
                document.getElementById(`question${question}`).classList.add('wrong');
                document.getElementById(`question${question}`).classList.remove('correct');
            }
            setTimeout(() => {
                if (currentPage < totalPages - 2) {
                    nextPage();
                } else if (currentPage === totalPages - 2) {
                    showResult();
                }
            }, 1500);
        }

        function playSoundcloud(btn, url) {
            var modal = document.getElementById('sc-modal');
            var iframe = document.getElementById('sc-iframe');
            iframe.src = url;
            modal.style.display = 'flex';
        }
        function closeModal() {
            var modal = document.getElementById('sc-modal');
            var iframe = document.getElementById('sc-iframe');
            iframe.src = '';
            modal.style.display = 'none';
        }
        window.onclick = function(event) {
            var modal = document.getElementById('sc-modal');
            if (event.target === modal) {
                closeModal();
            }
        }

        function nextPage() {
            document.getElementById(`page${currentPage}`).classList.remove('active');
            currentPage++;
            document.getElementById(`page${currentPage}`).classList.add('active');
            updateProgress();
        }

        function showResult() {
            document.getElementById(`page${currentPage}`).classList.remove('active');
            currentPage++;
            let score = calculateScore();
            let msg = "";
            if (score === 5) {
                document.getElementById(`page6`).classList.add('active');
                msg = "Você acertou todas as 5 perguntas!<br>Você me conhece perfeitamente! <span class='heart'>❤️</span>";
            } else if (score >= 3) {
                document.getElementById(`page7`).classList.add('active');
                msg = `Você acertou ${score} de 5 perguntas!<br>Quase perfeito! Vamos nos conhecer ainda melhor!`;
            } else {
                document.getElementById(`page7`).classList.add('active');
                msg = `Você acertou ${score} de 5 perguntas!<br>Precisamos de mais momentos juntos!`;
            }
            document.getElementById('result').innerHTML = msg;
            document.getElementById('score').textContent = score;
            updateProgress();
        }

        function calculateScore() {
            let score = 0;
            for (let i = 1; i <= 5; i++) {
                if (answers[i] === correctAnswers[i]) {
                    score++;
                }
            }
            return score;
        }

        function restartQuiz() {
            answers = {
                1: null,
                2: null,
                3: null,
                4: null,
                5: null
            };
            for (let i = 1; i <= 5; i++) {
                document.getElementById(`question${i}`).classList.remove('correct', 'wrong');
                const options = document.querySelectorAll(`#page${i} .option`);
                options.forEach(option => {
                    option.classList.remove('selected', 'correct', 'wrong');
                    option.disabled = false;
                });
            }
            document.getElementById(`page${currentPage}`).classList.remove('active');
            currentPage = 1;
            document.getElementById(`page${currentPage}`).classList.add('active');
            updateProgress();
        }

        updateProgress();
    </script>
</body>
</html>
