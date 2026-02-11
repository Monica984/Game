<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Dark Corridor</title>
<style>
  body {
    margin: 0;
    background: black;
    overflow: hidden;
  }

  canvas {
    display: block;
    margin: auto;
    background: black;
  }

  #jumpscare {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background: red;
    color: white;
    font-size: 60px;
    font-family: Arial, sans-serif;
    display: none;
    justify-content: center;
    align-items: center;
    z-index: 10;
  }
</style>
</head>

<body>

<div id="jumpscare">YOU WERE CAUGHT</div>
<canvas id="game" width="800" height="600"></canvas>

<script>
const canvas = document.getElementById("game");
const ctx = canvas.getContext("2d");
const jumpscare = document.getElementById("jumpscare");

// Player
let player = { x: 400, y: 300, size: 25, speed: 4 };

// Ghost
let ghost = { x: Math.random()*800, y: Math.random()*600, size: 40, speed: 1.8 };

// Controls
let keys = {};
document.addEventListener("keydown", e => keys[e.key] = true);
document.addEventListener("keyup", e => keys[e.key] = false);

function update() {
  // Player movement
  if (keys["w"]) player.y -= player.speed;
  if (keys["s"]) player.y += player.speed;
  if (keys["a"]) player.x -= player.speed;
  if (keys["d"]) player.x += player.speed;

  // Keep player inside screen
  player.x = Math.max(0, Math.min(775, player.x));
  player.y = Math.max(0, Math.min(575, player.y));

  // Ghost follows player
  if (ghost.x < player.x) ghost.x += ghost.speed;
  if (ghost.x > player.x) ghost.x -= ghost.speed;
  if (ghost.y < player.y) ghost.y += ghost.speed;
  if (ghost.y > player.y) ghost.y -= ghost.speed;

  // Collision check
  if (
    player.x < ghost.x + ghost.size &&
    player.x + player.size > ghost.x &&
    player.y < ghost.y + ghost.size &&
    player.y + player.size > ghost.y
  ) {
    triggerJumpscare();
  }
}

function draw() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);

  // Player
  ctx.fillStyle = "white";
  ctx.fillRect(player.x, player.y, player.size, player.size);

  // Ghost
  ctx.fillStyle = "red";
  ctx.fillRect(ghost.x, ghost.y, ghost.size, ghost.size);
}

function gameLoop() {
  update();
  draw();
  requestAnimationFrame(gameLoop);
}

function triggerJumpscare() {
  jumpscare.style.display = "flex";
  setTimeout(() => {
    location.reload();
  }, 1200);
}

gameLoop();
</script>

</body>
</html>
