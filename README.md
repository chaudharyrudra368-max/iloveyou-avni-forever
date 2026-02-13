<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>For Avni 💖</title>
<style>
  body {
    margin: 0;
    min-height: 100vh;
    background: radial-gradient(circle at top, #0b1d3a, #020111);
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', system-ui, sans-serif;
    color: #fff;
    text-align: center;
    overflow-y: auto; /* ✅ scrolling fixed */
  }

  h1 {
    margin-top: 30px;
    font-size: 2.6rem;
    animation: glow 2s ease-in-out infinite alternate;
  }

  @keyframes glow {
    from { text-shadow: 0 0 10px #fff, 0 0 20px #ff69b4; }
    to   { text-shadow: 0 0 20px #fff, 0 0 40px #ff1493; }
  }

  .card {
    background: rgba(255,255,255,0.15);
    padding: 18px;
    border-radius: 18px;
    width: 90%;
    max-width: 680px;
    margin: 16px auto;
    backdrop-filter: blur(10px);
    box-shadow: 0 10px 25px rgba(0,0,0,0.4);
  }

  button {
    background: #ff4d6d;
    border: none;
    color: white;
    padding: 12px 22px;
    border-radius: 24px;
    font-size: 16px;
    margin: 8px;
  }

  #noBtn {
    position: absolute;
    background: #ff9aa2;
  }

  .heart {
    position: fixed;
    bottom: -20px;
    font-size: 22px;
    animation: float 8s linear infinite;
    opacity: 0.8;
    pointer-events: none;
  }

  @keyframes float {
    from { transform: translateY(0); }
    to { transform: translateY(-120vh); }
  }

  .star {
    position: fixed;
    width: 2px;
    height: 2px;
    background: #fff;
    border-radius: 50%;
    opacity: 0.7;
    animation: twinkle 3s infinite ease-in-out alternate;
  }

  @keyframes twinkle {
    from { opacity: 0.2; }
    to { opacity: 1; }
  }

  #message {
    display: none;
    text-align: left;
    white-space: pre-line;
    line-height: 1.6;
    font-size: 15px;
    max-height: 60vh;                 /* ✅ scrollable area */
    overflow-y: auto;                /* ✅ scrolling enabled */
    -webkit-overflow-scrolling: touch;
  }

  canvas {
    position: fixed;
    inset: 0;
    pointer-events: none;
  }
</style>
</head>
<body>

<h1>Avni 💖</h1>

<div class="card">
  <p>Will you be my Valentine? 🌹</p>
  <button onclick="yesClicked()">Yes 💘</button>
  <button id="noBtn" ontouchstart="moveNo()" onmouseover="moveNo()">No 🙈</button>
</div>

<div id="message" class="card"></div>

<canvas id="fireworks"></canvas>

<audio id="piano" preload="auto">
  <source src="https://cdn.pixabay.com/audio/2022/03/15/audio_2f9f3d2e3b.mp3" type="audio/mpeg">
</audio>

<script>
  // Stars
  for (let i = 0; i < 120; i++) {
    const s = document.createElement('div');
    s.className = 'star';
    s.style.left = Math.random() * 100 + 'vw';
    s.style.top = Math.random() * 100 + 'vh';
    s.style.animationDelay = Math.random() * 3 + 's';
    document.body.appendChild(s);
  }

  // Floating hearts
  setInterval(() => {
    const h = document.createElement("div");
    h.className = "heart";
    h.innerHTML = "💖";
    h.style.left = Math.random() * 100 + "vw";
    document.body.appendChild(h);
    setTimeout(() => h.remove(), 8000);
  }, 700);

  function moveNo() {
    const btn = document.getElementById("noBtn");
    const x = Math.random() * (window.innerWidth - 120);
    const y = Math.random() * (window.innerHeight - 120);
    btn.style.left = x + "px";
    btn.style.top = y + "px";
  }

  const text = `Happy Valentine’s Day, Avni. 💖
This little page is just a small way to tell you something big:
You matter to me. A lot.

Thank you for being in my life. Thank you for your kindness, your warmth,
your presence that makes ordinary moments feel special.
I don’t love you only for how you make me feel,
I love and respect you for who you are.

This love isn’t temporary or seasonal.
It’s the quiet, steady kind that chooses you every single day.
No conditions. No doubts.

You are my peace, my comfort, my favorite thought,
and yeah, maybe my forever a little dramatic — but I mean it.
If forever had a name, it would sound like you.

I don’t promise perfection.
I promise loyalty, honesty, and respect.
No matter where life takes us, my heart will always recognize you as home.

Forever yours,
Rotra 💞`;

  function yesClicked() {
    const msg = document.getElementById("message");
    msg.style.display = "block";
    msg.textContent = "";
    typeWriter(msg, text, 0);
    document.getElementById("piano").play().catch(()=>{});
    launchFireworks();
  }

  function typeWriter(el, txt, i) {
    if (i < txt.length) {
      el.textContent += txt.charAt(i);
      setTimeout(() => typeWriter(el, txt, i + 1), 18);
    }
  }

  // Fireworks
  const canvas = document.getElementById('fireworks');
  const ctx = canvas.getContext('2d');
  function resize() {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
  }
  window.addEventListener('resize', resize);
  resize();

  function launchFireworks() {
    let particles = [];
    for (let i = 0; i < 140; i++) {
      particles.push({
        x: canvas.width / 2,
        y: canvas.height / 2,
        vx: (Math.random() - 0.5) * 7,
        vy: (Math.random() - 0.5) * 7,
        life: 60
      });
    }
    function animate() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      particles.forEach(p => {
        ctx.beginPath();
        ctx.arc(p.x, p.y, 2, 0, Math.PI * 2);
        ctx.fillStyle = 'rgba(255,182,193,0.9)';
        ctx.fill();
        p.x += p.vx;
        p.y += p.vy;
        p.life--;
      });
      particles = particles.filter(p => p.life > 0);
      if (particles.length) requestAnimationFrame(animate);
    }
    animate();
  }
</script>

</body>
</html>
