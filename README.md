<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Quiz App</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 20px; }
    .question { margin-bottom: 15px; }
    .options label { display: block; margin-bottom: 5px; }
    button { padding: 8px 12px; margin-top: 10px; }
    .result { margin-top: 20px; font-weight: bold; }
    .correct { color: green; }
    .incorrect { color: red; }
  </style>
</head>
<body>
  <h2>Quiz App</h2>
  <form id="quizForm"></form>
  <button onclick="submitQuiz()">Submit</button>
  <div id="result"></div>

  <script>
    const questions = [
      { q: "What does HTML stand for?", options: ["Hyperlinks and Text Markup Language", "Home Tool Markup Language", "Hyper Text Markup Language", "Hyper Text Managing Links"], answer: 2 },
      { q: "Which language runs in a web browser?", options: ["Java", "C", "Python", "JavaScript"], answer: 3 },
      { q: "What does CSS stand for?", options: ["Creative Style Sheets", "Cascading Style Sheets", "Computer Style Sheets", "Colorful Style Sheets"], answer: 1 },
      { q: "Inside which HTML element do we put the JavaScript?", options: ["<js>", "<scripting>", "<script>", "<javascript>"], answer: 2 },
      { q: "Which property is used to change background color in CSS?", options: ["color", "background-color", "bgColor", "background"], answer: 1 }
    ];

    const form = document.getElementById("quizForm");
    function loadQuiz() {
      questions.forEach((item, i) => {
        let div = document.createElement("div");
        div.classList.add("question");
        div.innerHTML = `<p>${i+1}. ${item.q}</p>`;
        item.options.forEach((opt, j) => {
          div.innerHTML += `
            <label><input type="radio" name="q${i}" value="${j}"> ${opt}</label>`;
        });
        form.appendChild(div);
      });
    }
    loadQuiz();

    function submitQuiz() {
      let score = 0, resultHTML = "";
      questions.forEach((item, i) => {
        let selected = document.querySelector(`input[name="q${i}"]:checked`);
        if (selected) {
          if (parseInt(selected.value) === item.answer) {
            score++;
            resultHTML += `<p class="correct">${i+1}. Correct</p>`;
          } else {
            resultHTML += `<p class="incorrect">${i+1}. Incorrect (Correct: ${item.options[item.answer]})</p>`;
          }
        } else {
          resultHTML += `<p class="incorrect">${i+1}. Not Answered (Correct: ${item.options[item.answer]})</p>`;
        }
      });
      document.getElementById("result").innerHTML = 
        `<p>Your Score: ${score}/${questions.length}</p>` + resultHTML;
    }
  </script>
</body>
</html>

