<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Multiplication Quiz</title>
</head>
<body>

<div id="quiz">
  <div id="start-page">
    <h2>Welcome to the Multiplication Quiz!</h2>
    <p>Click the button below to start the quiz.</p>
    <button onclick="startQuiz()">Start Quiz</button>
  </div>

  <div id="question-page" style="display: none;">
    <div id="question"></div>
    <input type="number" id="answer" placeholder="Enter your answer" inputmode="numeric">
    <button onclick="submitAnswer()">Submit Answer</button>
  </div>

  <div id="result-page" style="display: none;">
    <h2>Your Score:</h2>
    <div id="score"></div>
  </div>
</div>

<script>
  // Define multiplication questions and answers
  const questions = [];
  for (let i = 2; i <= 9; i++) {
    for (let j = 2; j <= 9; j++) {
      questions.push({ question: `${i} X  ${j} = `, answer: i * j });
    }
  }

  // Randomize questions order
  shuffle(questions);

  let currentQuestion = 0;
  let score = 0;

  function startQuiz() {
    document.getElementById('start-page').style.display = 'none';
    loadQuestion();
  }

  function loadQuestion() {
    if (currentQuestion < questions.length) {
      document.getElementById('question').innerText = questions[currentQuestion].question;
      document.getElementById('answer').value = '';
      document.getElementById('question-page').style.display = 'block';
    } else {
      showResult();
    }
  }

  function submitAnswer() {
    const userAnswer = parseInt(document.getElementById('answer').value);
    if (!isNaN(userAnswer)) {
      if (userAnswer === questions[currentQuestion].answer) {
        score++;
      }
      currentQuestion++;
      loadQuestion();
    } else {
      alert('Please enter a valid number.');
    }
  }

  function showResult() {
    document.getElementById('question-page').style.display = 'none';
    document.getElementById('result-page').style.display = 'block';
    document.getElementById('score').innerText = `${score} out of ${questions.length}`;
  }

  // Function to shuffle array elements (Fisher-Yates shuffle algorithm)
  function shuffle(array) {
    for (let i = array.length - 1; i > 0; i--) {
      const j = Math.floor(Math.random() * (i + 1));
      [array[i], array[j]] = [array[j], array[i]];
    }
  }
</script>

</body>
</html>
