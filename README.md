# Valentine
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Be My Valentine?</title>
  <style>
    body {
      margin: 0;
      height: 100vh;
      overflow: hidden;
      display: flex;
      justify-content: center;
      align-items: center;
      background: linear-gradient(135deg, #ff9a9e, #fad0c4);
      font-family: Arial, sans-serif;
    }

    .card {
      background: white;
      padding: 40px;
      border-radius: 20px;
      text-align: center;
      box-shadow: 0 20px 40px rgba(0,0,0,0.2);
      z-index: 2;
    }

    h1 {
      color: #ff4d6d;
      font-size: 2.2rem;
      margin-bottom: 10px;
    }

    h2 {
      color: #ff758f;
      font-size: 1.2rem;
      margin-bottom: 30px;
      font-weight: normal;
    }

    button {
      font-size: 1.2rem;
      padding: 12px 25px;
      border: none;
      border-radius: 30px;
      cursor: pointer;
      margin: 10px;
      transition: 0.2s ease;
    }

    #yes {
      background: #ff4d6d;
      color: white;
    }

    #no {
      background: #ccc;
      position: relative;
    }

    #message {
      margin-top: 20px;
      font-size: 1.5rem;
      color: #ff4d6d;
      display: none;
    }

    canvas {
      position: fixed;
      top: 0;
      left: 0;
      pointer-events: none;
      z-index: 1;
    }
  </style>
</head>
<body>

  <canvas id="fireworks"></canvas>

  <div class="card">
    <h1>Will you be my Valentine? 💘</h1>
    <h2>Mishti — <em>queen of the whole universe</em> 👑🌌</h2>

    <button id="yes">Yes 💖</button>
    <button id="no">No 😢</button>

    <div id="message">YAYYY!! THE UNIVERSE CELEBRATES 🎆💞</div>
  </div>

  <script>
    const noBtn = document.getElementById("no");
    const yesBtn = document.getElementById("yes");
    const message = document.getElementById("message");

    // No button escape
    noBtn.addEventListener("mouseover", () => {
      const x = Math.random() * 200 - 100;
      const y = Math.random() * 200 - 100;
      noBtn.style.transform = `translate(${x}px, ${y}px)`;
    });

    // Fireworks setup
    const canvas = document.getElementById("fireworks");
    const ctx = canvas.getContext("2d");
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;

    let particles = [];

    function createFirework(x, y) {
      for (let i = 0; i < 80; i++) {
        particles.push({
          x,
          y,
          angle: Math.random() * Math.PI * 2,
          speed: Math.random() * 6 + 2,
          radius: 2,
          life: 100,
          color: `hsl(${Math.random() * 360}, 100%, 60%)`
        });
      }
    }

    function animateFireworks() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      particles.forEach((p, i) => {
        p.x += Math.cos(p.angle) * p.speed;
        p.y += Math.sin(p.angle) * p.speed;
        p.life--;

        ctx.beginPath();
        ctx.arc(p.x, p.y, p.radius, 0, Math.PI * 2);
        ctx.fillStyle = p.color;
        ctx.fill();

        if (p.life <= 0) particles.splice(i, 1);
      });
      requestAnimationFrame(animateFireworks);
    }

    animateFireworks();

    yesBtn.addEventListener("click", () => {
      message.style.display = "block";
      yesBtn.style.display = "none";
      noBtn.style.display = "none";

      for (let i = 0; i < 6; i++) {
        setTimeout(() => {
          createFirework(
            Math.random() * canvas.width,
            Math.random() * canvas.height / 2
          );
        }, i * 300);
      }
    });

    window.addEventListener("resize", () => {
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    });
  </script>

</body>
</html>
