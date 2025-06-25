
<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <title>Ucapan Ulang Tahun</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      font-family: 'Arial', sans-serif;
      background: #000;
      color: white;
      text-align: center;
      overflow: hidden;
    }
    .screen {
      display: none;
      justify-content: center;
      align-items: center;
      height: 100vh;
      flex-direction: column;
    }
    .screen.active {
      display: flex;
    }
    button {
      margin-top: 20px;
      padding: 12px 24px;
      font-size: 18px;
      border: none;
      border-radius: 8px;
      background-color: #ff4081;
      color: white;
      cursor: pointer;
    }
    .responsive-img {
      max-width: 300px;
      width: 100%;
      height: auto;
      border-radius: 16px;
      margin-bottom: 20px;
    }

    .fireworks {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
      z-index: 0;
    }
    .message-box {
      background: rgba(255, 255, 255, 0.5);
      color: black;
      padding: 30px;
      border-radius: 20px;
      font-size: 24px;
      margin-top: 20px;
      z-index: 1;
    }
  </style>
</head>
<body>

<!-- Halaman 1: Mulai -->
<div id="screen1" class="screen active">
  <h1>Selamat Datang!</h1>
  <button onclick="nextScreen(2)">Mulai</button>
</div>

<!-- Halaman 2: Foto dan lanjut -->
<div id="screen2" class="screen">
  <img 
    src="https://raw.githubusercontent.com/luk24/foto_kekasih/main/WhatsApp%20Image%202025-06-25%20at%2020.24.06.jpeg" 
    alt="Foto Kekasih" 
    class="responsive-img"
  >
  <button onclick="nextScreen(3)">Lanjut</button>
</div>

<!-- Halaman 3: Petasan dan pesan -->
<div id="screen3" class="screen">
  <canvas id="fireworks" class="fireworks"></canvas>
  <div class="message-box">Selamat ulang tahun sayangku 🎉</div>
</div>

<audio id="birthdayMusic" src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3"></audio>

<script>
  function nextScreen(screenNumber) {
    document.querySelectorAll('.screen').forEach(el => el.classList.remove('active'));
    document.getElementById('screen' + screenNumber).classList.add('active');

    if (screenNumber === 3) {
      startFireworks();
      document.getElementById('birthdayMusic').play();
    }
  }

  function startFireworks() {
    const canvas = document.getElementById('fireworks');
    const ctx = canvas.getContext('2d');
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;

    let particles = [];

    function createParticle(x, y) {
      for (let i = 0; i < 100; i++) {
        particles.push({
          x: x,
          y: y,
          radius: Math.random() * 2 + 1,
          color: `hsl(${Math.random() * 360}, 100%, 50%)`,
          angle: Math.random() * Math.PI * 2,
          speed: Math.random() * 4 + 1,
          life: 100
        });
      }
    }

    function updateParticles() {
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
    }

    setInterval(() => {
      const x = Math.random() * canvas.width;
      const y = Math.random() * canvas.height / 2;
      createParticle(x, y);
    }, 500);

    function animate() {
      updateParticles();
      requestAnimationFrame(animate);
    }

    animate();
  }
</script>

</body>
</html>
