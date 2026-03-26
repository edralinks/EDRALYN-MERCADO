# EDRALYN-MERCADO
BS MECHATRONICS ENGINEERING

# Hi there 👋
## I'm Ralph Neil Maranan

💻 Aspiring Mechatronics Engineer  
📍 Philippines  
🎓 Batangas State University  

---
<!DOCTYPE html>
<html>
<head>
  <title>Pixel Dino Runner</title>
  <style>
    body {
      background: #111;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }

    canvas {
      background: #222;
      border: 3px solid #fff;
      image-rendering: pixelated;
    }
  </style>
</head>
<body>

<canvas id="game" width="600" height="200"></canvas>

<script>
const canvas = document.getElementById("game");
const ctx = canvas.getContext("2d");

let dino = {
  x: 50,
  y: 150,
  w: 20,
  h: 20,
  vy: 0,
  jumping: false
};

let gravity = 0.8;

let obstacle = {
  x: 600,
  y: 150,
  w: 20,
  h: 20
};

let score = 0;

document.addEventListener("keydown", () => {
  if (!dino.jumping) {
    dino.vy = -12;
    dino.jumping = true;
  }
});

function update() {
  // Dino physics
  dino.y += dino.vy;
  dino.vy += gravity;

  if (dino.y >= 150) {
    dino.y = 150;
    dino.jumping = false;
  }

  // Obstacle movement
  obstacle.x -= 5;
  if (obstacle.x < -20) {
    obstacle.x = 600;
    score++;
  }

  // Collision
  if (
    dino.x < obstacle.x + obstacle.w &&
    dino.x + dino.w > obstacle.x &&
    dino.y < obstacle.y + obstacle.h &&
    dino.y + dino.h > obstacle.y
  ) {
    alert("Game Over! Score: " + score);
    location.reload();
  }
}

function draw() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);

  // Dino (pixel style)
  ctx.fillStyle = "#00ff88";
  ctx.fillRect(dino.x, dino.y, dino.w, dino.h);

  // Obstacle
  ctx.fillStyle = "#ff4444";
  ctx.fillRect(obstacle.x, obstacle.y, obstacle.w, obstacle.h);

  // Ground
  ctx.fillStyle = "#fff";
  ctx.fillRect(0, 170, 600, 5);

  // Score
  ctx.fillStyle = "#fff";
  ctx.font = "12px monospace";
  ctx.fillText("Score: " + score, 10, 20);
}

function gameLoop() {
  update();
  draw();
  requestAnimationFrame(gameLoop);
}

gameLoop();
</script>

</body>
</html>
