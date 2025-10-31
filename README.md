<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Emergency Kit Game</title>
<style>
body {
font-family: Arial, sans-serif;
background: linear-gradient(to right, #f0f8ff, #e6f7ff);
text-align: center;
padding: 30px;
}
h1 {
color: #005580;
}
.disaster-select, .items, .kit, .result {
margin: 20px auto;
max-width: 500px;
}
button {
background: #0099cc;
color: white;
border: none;
padding: 10px 20px;
border-radius: 10px;
margin: 5px;
cursor: pointer;
}
button:hover {
background: #007399;
}
.item-btn.selected {
background: #4CAF50;
}
.wrong {
background: #cc0000 !important;
}
.hidden {
display: none;
}
#score, #timer {
font-size: 18px;
color: #004466;
font-weight: bold;
margin: 10px;
}
</style>
</head>
<body>
<h1>Emergency Kit Challenge!</h1>
<div id="score">Score: 100</div>
<div id="timer">Time Left: 60s</div>
<div class="disaster-select">
<h3>Select a disaster:</h3>
<button onclick="chooseDisaster('earthquake')">Earthquake</button>
<button onclick="chooseDisaster('flood')">Flood</button>
<button onclick="chooseDisaster('cyclone')">Cyclone</button>
</div>


<div class="items hidden">
<h3>Pack your emergency kit:</h3>
<div id="itemsList"></div>
<button onclick="checkKit()">Done Packing!</button>
</div>


<div class="result hidden">
<h3 id="resultText"></h3>
<button onclick="restartGame()">Play Again</button>
</div>


<audio id="correctSound" src="https://cdn.pixabay.com/download/audio/2022/03/15/audio_c5d05ef64a.mp3?filename=correct-2-46134.mp3"></audio>
