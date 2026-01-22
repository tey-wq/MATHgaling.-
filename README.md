# MATHgaling.-
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>MathGaling</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: linear-gradient(to bottom right, #2196f3, #9c27b0);
  color: white;
  text-align: center;
}
.screen { display: none; padding: 30px; }
.active { display: block; }
button {
  padding: 12px 25px;
  margin: 10px;
  font-size: 16px;
  border: none;
  border-radius: 25px;
}
.start { background: #00e676; color: black; }
.easy { background: #2196f3; }
.medium { background: #4caf50; }
.hard { background: #9c27b0; }

.color-btn {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  border: none;
  margin: 15px;
}
.blue { background: #2196f3; }
.green { background: #4caf50; }
.purple { background: #9c27b0; }

.option {
  background: white;
  color: black;
  padding: 12px;
  margin: 8px;
  border-radius: 15px;
}

.fade { animation: fade 0.4s; }
@keyframes fade {
  from { opacity: 0; }
  to { opacity: 1; }
}
</style>
</head>

<body>

<!-- FRONT SCREEN -->
<div class="screen active fade" id="front">
  <h1>MathGaling</h1>
  <p>Grade 9 Challenge</p>
  <button class="start" onclick="show('difficulty')">START</button>
</div>

<!-- DIFFICULTY -->
<div class="screen fade" id="difficulty">
  <h2>Select Difficulty</h2>
  <button class="easy" onclick="setDifficulty('easy')">Easy</button>
  <button class="medium" onclick="setDifficulty('medium')">Medium</button>
  <button class="hard" onclick="setDifficulty('hard')">Difficult</button>
</div>

<!-- COLORS -->
<div class="screen fade" id="colors">
  <h2>Select a Color</h2>
  <button class="color-btn blue" onclick="loadQuestion(0)"></button>
  <button class="color-btn green" onclick="loadQuestion(1)"></button>
  <button class="color-btn purple" onclick="loadQuestion(2)"></button>
</div>

<!-- QUESTION -->
<div class="screen fade" id="question">
  <h2 id="qtext"></h2>
  <div id="options"></div>
</div>

<!-- RESULT -->
<div class="screen fade" id="result">
  <h2 id="resultText"></h2>
  <button id="okBtn" onclick="okClick()" style="display:none;">OK</button>
  <button id="keepBtn" onclick="show('colors')" style="display:none;">Keep Playing</button>
</div>

<!-- SOLUTION -->
<div class="screen fade" id="solution">
  <h2>Solution</h2>
  <p id="solutionText"></p>
  <button onclick="show('difficulty')">OK</button>
</div>

<script>
let difficulty = "";
let currentQ;

// QUESTIONS (GRADE 9)
const data = {
  easy: [
    { q: "Solve: x + 5 = 12", options: ["x=5","x=6","x=7","x=8"], answer:2, solution:"x + 5 = 12 → x = 12 − 5 → x = 7" },
    { q: "Find 3x if x=4", options:["7","10","12","14"], answer:2, solution:"3x = 3*4 = 12" },
    { q: "Half of 14?", options:["5","6","7","8"], answer:2, solution:"14 ÷ 2 = 7" }
  ],
  medium: [
    { q: "Solve: 2x + 4 = 14", options:["x=4","x=5","x=6","x=7"], answer:1, solution:"2x + 4 = 14 → 2x = 10 → x = 5" },
    { q: "Midpoint of (2,6) and (8,10)?", options:["(4,8)","(5,8)","(6,8)","(5,6)"], answer:1, solution:"((2+8)/2, (6+10)/2) = (5,8)" },
    { q: "Solve: 5x = 25", options:["3","4","5","6"], answer:2, solution:"5x = 25 → x = 5" }
  ],
  hard: [
    { q: "Solve: 3x−7=11", options:["x=4","x=5","x=6","x=7"], answer:2, solution:"3x−7=11 → 3x=18 → x=6" },
    { q: "Base of triangle =12, find midline", options:["4","5","6","8"], answer:2, solution:"Midline = 1/2 of base → 12 ÷ 2 = 6" },
    { q: "Solve: 4x+2=18", options:["3","4","5","6"], answer:1, solution:"4x+2=18 → 4x=16 → x=4" }
  ]
};

let correctAnswer = false;

function show(id){
  document.querySelectorAll('.screen').forEach(s=>s.classList.remove('active'));
  document.getElementById(id).classList.add('active');
}

function setDifficulty(d){
  difficulty = d;
  show('colors');
}

function loadQuestion(i){
  currentQ = data[difficulty][i];
  document.getElementById("qtext").innerText = currentQ.q;

  let html = "";
  currentQ.options.forEach((o,idx)=>{
    html += `<div class="option" onclick="check(${idx})">${o}</div>`;
  });
  document.getElementById("options").innerHTML = html;
  show('question');
}

function check(choice){
  if(choice === currentQ.answer){
    correctAnswer = true;
    document.getElementById("resultText").innerText = "✅ Correct!";
    document.getElementById("okBtn").style.display = "inline-block";
    document.getElementById("keepBtn").style.display = "inline-block";
  } else {
    correctAnswer = false;
    document.getElementById("resultText").innerText = "❌ Wrong!";
    document.getElementById("okBtn").style.display = "inline-block";
    document.getElementById("keepBtn").style.display = "none";
  }
  document.getElementById("solutionText").innerText = currentQ.solution;
  show('result');
}

function okClick(){
  if(correctAnswer){
    show('colors'); // Pag tama, babalik sa color selection
  } else {
    show('solution'); // Pag mali, punta sa solution
  }
}
</script>

</body>
</html>
