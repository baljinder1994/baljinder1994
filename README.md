<!DOCTYPE html>
<html>
<head>
    <title>Quiz Game</title>
    <style>
         body {
            font-family: Arial, sans-serif;
            text-align: center;
        }

        h1 {
            color: #333;
        }

        #quiz-container {
            max-width: 500px;
            margin: 0 auto;
            background-color: #f7f7f7;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
        }

        #question {
            font-size: 18px;
            margin-bottom: 10px;
        }

        ul {
            list-style: none;
            padding: 0;
        }

        li {
            margin: 10px 0;
        }

        button {
            background-color: #3498db;
            color: #fff;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
        }

        button:hover {
            background-color: #2374b6;
        }

        #result {
            font-size: 20px;
            font-weight: bold;
        }
    </style>
</head>
<body>
    <h1>Quiz Game</h1>
    <div id="quiz-container">
        <h2 id="question">Question 1: What is the capital of France?</h2>
        <ul id="choices">
            <li><button onclick="checkAnswer('Paris')">Paris</button></li>
            <li><button onclick="checkAnswer('London')">London</button></li>
            <li><button onclick="checkAnswer('Berlin')">Berlin</button></li>
        </ul>
    </div>
    <p id="result">Score: 0</p>

    <script>
        // Define quiz questions and answers
        const questions = [
            {
                question: "What is the capital of France?",
                choices: ["Paris", "London", "Berlin"],
                correctAnswer: "Paris",
            },
            {
                question: "Which planet is known as the Red Planet?",
                choices: ["Earth", "Mars", "Venus"],
                correctAnswer: "Mars",
            },
            {
                question: "What is the largest mammal in the world?",
                choices: ["Elephant", "Blue Whale", "Giraffe"],
                correctAnswer: "Blue Whale",
            },
        ];

        let currentQuestionIndex = 0;
        let score = 0;

        // Function to display the current question
        function displayQuestion() {
            const questionText = document.getElementById("question");
            const choicesList = document.getElementById("choices");
            const currentQuestion = questions[currentQuestionIndex];

            questionText.textContent = `Question ${currentQuestionIndex + 1}: ${currentQuestion.question}`;
            choicesList.innerHTML = '';

            currentQuestion.choices.forEach(choice => {
                const li = document.createElement("li");
                const button = document.createElement("button");
                button.textContent = choice;
                button.onclick = () => checkAnswer(choice);
                li.appendChild(button);
                choicesList.appendChild(li);
            });
        }

        // Function to check the selected answer
        function checkAnswer(selectedAnswer) {
            const currentQuestion = questions[currentQuestionIndex];

            if (selectedAnswer === currentQuestion.correctAnswer) {
                score++;
            }

            currentQuestionIndex++;

            if (currentQuestionIndex < questions.length) {
                displayQuestion();
            } else {
                endGame();
            }

            updateScore();
        }

        // Function to update the user's score
        function updateScore() {
            const resultText = document.getElementById("result");
            resultText.textContent = `Score: ${score}`;
        }

        // Function to end the game
        function endGame() {
            const quizContainer = document.getElementById("quiz-container");
            quizContainer.innerHTML = `<h2>Game Over!</h2><p>Your final score is: ${score}/${questions.length}</p>`;
        }

        // Start the game
        displayQuestion();
    </script>
</body>
</html>
