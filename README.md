<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<title>Para Diana 💛</title>

<style>
body {
    margin: 0;
    overflow: hidden;
    font-family: Arial, sans-serif;
    text-align: center;
    color: white;
    background: linear-gradient(to top, #1a1a2e, #16213e, #0f3460);
}

/* Texto */
.container {
    position: relative;
    z-index: 2;
    top: 50px;
}

h1 {
    font-size: 2.5em;
}

.card {
    background: rgba(255,255,255,0.1);
    margin: 20px auto;
    padding: 20px;
    border-radius: 20px;
    width: 85%;
    max-width: 400px;
    backdrop-filter: blur(10px);
}

img {
    width: 100%;
    border-radius: 15px;
    margin-top: 10px;
}

/* Flores */
.flower {
    position: absolute;
    font-size: 25px;
    animation: fall linear infinite;
}

@keyframes fall {
    0% { transform: translateY(-10vh); opacity: 1; }
    100% { transform: translateY(110vh); opacity: 0; }
}

/* Canvas fireworks */
canvas {
    position: fixed;
    top: 0;
    left: 0;
    z-index: 1;
}
</style>
</head>

<body>

<canvas id="fireworks"></canvas>

<div class="container">
    <h1>🌼 Para Diana 🌼</h1>

    <div class="card">
        <p>Desde el <strong>28 de marzo de 2020</strong> 💛</p>
        <p>Llevamos juntas:</p>
        <p id="time"></p>

        <img src="https://photos.app.goo.gl/zVbyxmPtWbY3jF5SA">

        <p>
        Si existe un lugar como San Junipero…<br>
        quiero vivirlo contigo una y otra vez ✨💛
        </p>
    </div>
</div>

<!-- Música YouTube -->
<iframe width="0" height="0"
src="src="https://www.youtube.com/embed/j2F4INQFjEI?autoplay=1&loop=1&playlist=j2F4INQFjEI""
frameborder="0" allow="autoplay"></iframe>

<script>
// CONTADOR
const startDate = new Date("2020-03-28");
const now = new Date();

let years = now.getFullYear() - startDate.getFullYear();
let months = now.getMonth() - startDate.getMonth();
let days = now.getDate() - startDate.getDate();

if (days < 0) {
    months--;
    const lastMonth = new Date(now.getFullYear(), now.getMonth(), 0);
    days += lastMonth.getDate();
}

if (months < 0) {
    years--;
    months += 12;
}

document.getElementById("time").innerText =
`${years} años, ${months} meses y ${days} días 💕`;

// FLORES cayendo
function createFlower() {
    const flower = document.createElement("div");
    flower.innerHTML = "🌼";
    flower.classList.add("flower");

    flower.style.left = Math.random() * 100 + "vw";
    flower.style.animationDuration = (3 + Math.random() * 5) + "s";

    document.body.appendChild(flower);

    setTimeout(() => {
        flower.remove();
    }, 8000);
}
setInterval(createFlower, 300);

// FUEGOS ARTIFICIALES
const canvas = document.getElementById("fireworks");
const ctx = canvas.getContext("2d");

canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

let particles = [];

function createFirework() {
    let x = Math.random() * canvas.width;
    let y = Math.random() * canvas.height / 2;

    for (let i = 0; i < 50; i++) {
        particles.push({
            x: x,
            y: y,
            vx: (Math.random() - 0.5) * 5,
            vy: (Math.random() - 0.5) * 5,
            alpha: 1
        });
    }
}

function updateFireworks() {
    ctx.fillStyle = "rgba(0,0,0,0.2)";
    ctx.fillRect(0, 0, canvas.width, canvas.height);

    particles.forEach((p, i) => {
        p.x += p.vx;
        p.y += p.vy;
        p.alpha -= 0.01;

        ctx.fillStyle = "rgba(255,215,0," + p.alpha + ")";
        ctx.beginPath();
        ctx.arc(p.x, p.y, 2, 0, Math.PI * 2);
        ctx.fill();

        if (p.alpha <= 0) {
            particles.splice(i, 1);
        }
    });

    requestAnimationFrame(updateFireworks);
}

setInterval(createFirework, 800);
updateFireworks();
</script>

</body>
</html>

