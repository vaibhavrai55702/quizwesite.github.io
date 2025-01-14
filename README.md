<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quiz Website</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 0;
            padding: 0;
        }
        #front-page {
            background-color: black;
            color: white;
            height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
        }
        .container {
            margin: 20px auto;
            padding: 20px;
            background-color: rgba(255, 255, 255, 0.9);
            border-radius: 8px;
            width: 80%;
            max-width: 600px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }
        h1 {
            color: blue;
        }
        h2 {
            color: red;
        }
        .options button {
            display: block;
            margin: 10px auto;
            padding: 10px 20px;
            border: none;
            background-color: #007bff;
            color: white;
            border-radius: 5px;
            cursor: pointer;
            width: 80%;
        }
        .options button:hover {
            background-color: #0056b3;
        }
        .background {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            background-size: cover;
            background-position: center;
        }
    </style>
</head>
<body>
    <div id="front-page">
        <h1>Quiz Website</h1>
        <h2>Select a Level:</h2>
        <button onclick="startQuiz(1)">Level 1: General Knowledge</button>
        <button onclick="startQuiz(2)">Level 2: Maths</button>
        <button onclick="startQuiz(3)">Level 3: Geography</button>
    </div>

    <div class="background" id="background"></div>

    <div class="container" id="quiz-container" style="display:none">
    </div>

    <script>
        const questions = {
            1: [
                { q: "What is the capital of France?", options: ["Paris", "London", "Berlin", "Madrid"], answer: 0 },
                { q: "Which planet is known as the Red Planet?", options: ["Earth", "Mars", "Jupiter", "Venus"], answer: 1 },
                { q: "What is the largest mammal?", options: ["Elephant", "Whale", "Shark", "Giraffe"], answer: 1 },
                { q: "How many continents are there?", options: ["5", "6", "7", "8"], answer: 2 },
                { q: "What is the boiling point of water?", options: ["90°C", "100°C", "80°C", "120°C"], answer: 1 }
            ],
            2: [
                { q: "What is 5 + 3?", options: ["5", "8", "9", "7"], answer: 1 },
                { q: "What is 12 / 4?", options: ["1", "2", "3", "4"], answer: 2 },
                { q: "What is 9 x 2?", options: ["18", "20", "15", "19"], answer: 0 },
                { q: "What is 15 - 7?", options: ["7", "9", "8", "10"], answer: 2 },
                { q: "What is 10% of 100?", options: ["1", "5", "10", "20"], answer: 2 }
            ],
            3: [
                { q: "What is the largest desert in the world?", options: ["Sahara", "Antarctica", "Gobi", "Kalahari"], answer: 1 },
                { q: "Which is the longest river in the world?", options: ["Nile", "Amazon", "Yangtze", "Mississippi"], answer: 1 },
                { q: "What is the smallest country?", options: ["Vatican City", "Monaco", "San Marino", "Liechtenstein"], answer: 0 },
                { q: "Which country has the most population?", options: ["India", "USA", "China", "Brazil"], answer: 2 },
                { q: "What is the capital of Australia?", options: ["Sydney", "Melbourne", "Canberra", "Brisbane"], answer: 2 }
            ]
        };

        let currentQuestionIndex = 0;
        let score = 0;
        let currentLevel = 0;

        function startQuiz(level) {
            currentLevel = level;
            currentQuestionIndex = 0;
            score = 0;

            // Hide front page and show quiz container
            document.getElementById('front-page').style.display = 'none';
            document.getElementById('quiz-container').style.display = 'block';

            // Change the background image based on the level
            const background = document.getElementById('background');
            if (level === 1) {
                background.style.backgroundImage = "url('https://www.tajmahal.gov.in/images/banners/1.jpg')";
            } else if (level === 2) {
                background.style.backgroundImage = "url('https://images.unsplash.com/photo-1518216049389-a6ce1f175e59?q=80&w=2000&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D')";
            } else if (level === 3) {
                background.style.backgroundImage = "url('https://upload.wikimedia.org/wikipedia/commons/1/1b/%C3%8Dndios_isolados_no_Acre_5.jpg')";
            }

            showQuestion();
        }

        function showQuestion() {
            const container = document.getElementById('quiz-container');
            const question = questions[currentLevel][currentQuestionIndex];
            container.innerHTML = `
                <h2>Question ${currentQuestionIndex + 1}</h2>
                <p>${question.q}</p>
                <div class="options">
                    ${question.options.map((option, index) => `
                        <button onclick="checkAnswer(${index})">${option}</button>
                    `).join('')}
                </div>
            `;
        }

        function checkAnswer(selectedIndex) {
            const question = questions[currentLevel][currentQuestionIndex];
            if (selectedIndex === question.answer) {
                score++;
            }
            currentQuestionIndex++;
            if (currentQuestionIndex < questions[currentLevel].length) {
                showQuestion();
            } else {
                showResult();
            }
        }

        function showResult() {
            const container = document.getElementById('quiz-container');
            container.innerHTML = `
                <h2>Your Score: ${score}/${questions[currentLevel].length}</h2>
                <div class="result">${score === questions[currentLevel].length ? '🎉 Perfect Score!' : 'Good Job!'}</div>
                <button onclick="location.reload()">Try Again</button>
            `;
        }
    </script>
</body>
</html>
