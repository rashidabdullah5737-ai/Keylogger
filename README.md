<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Abdullah Rashid | Cybersecurity Portfolio</title>
<link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=Orbitron:wght@400;700;900&display=swap" rel="stylesheet">
<style>
  :root {
    --green: #00ff9c;
    --green-dim: #00cc7a;
    --green-ghost: rgba(0,255,156,0.07);
    --green-glow: 0 0 10px #00ff9c88, 0 0 30px #00ff9c33;
    --bg: #000;
    --bg2: #080d0a;
    --border: 1px solid #00ff9c44;
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    font-family: 'Share Tech Mono', monospace;
    background: var(--bg);
    color: var(--green);
    overflow-x: hidden;
    cursor: crosshair;
  }

  /* ── SCANLINE OVERLAY ── */
  body::before {
    content: '';
    position: fixed; inset: 0;
    background: repeating-linear-gradient(
      to bottom,
      transparent 0px,
      transparent 3px,
      rgba(0,0,0,0.18) 3px,
      rgba(0,0,0,0.18) 4px
    );
    pointer-events: none;
    z-index: 9999;
  }

  canvas#matrix {
    position: fixed; top: 0; left: 0;
    z-index: 0;
    opacity: 0.18;
  }

  /* ── HEADER ── */
  header {
    position: relative;
    z-index: 10;
    text-align: center;
    padding: 70px 20px 40px;
    border-bottom: var(--border);
    background: linear-gradient(to bottom, rgba(0,255,156,0.04), transparent);
  }

  .glitch {
    font-family: 'Orbitron', sans-serif;
    font-size: clamp(32px, 6vw, 64px);
    font-weight: 900;
    letter-spacing: 6px;
    text-transform: uppercase;
    position: relative;
    display: inline-block;
    text-shadow: var(--green-glow);
    animation: flicker 6s infinite;
  }

  .glitch::before,
  .glitch::after {
    content: attr(data-text);
    position: absolute; top: 0; left: 0;
    width: 100%; height: 100%;
  }
  .glitch::before {
    color: #ff0044;
    clip-path: polygon(0 30%, 100% 30%, 100% 50%, 0 50%);
    transform: translateX(-3px);
    animation: glitch1 4s infinite;
  }
  .glitch::after {
    color: #00cfff;
    clip-path: polygon(0 60%, 100% 60%, 100% 80%, 0 80%);
    transform: translateX(3px);
    animation: glitch2 4s infinite;
  }

  @keyframes glitch1 {
    0%,94%,100% { transform: translateX(0); opacity: 0; }
    95% { transform: translateX(-4px); opacity: 1; }
    97% { transform: translateX(4px); opacity: 1; }
    99% { transform: translateX(0); opacity: 0; }
  }
  @keyframes glitch2 {
    0%,92%,100% { transform: translateX(0); opacity: 0; }
    93% { transform: translateX(5px); opacity: 1; }
    96% { transform: translateX(-3px); opacity: 1; }
    98% { transform: translateX(0); opacity: 0; }
  }
  @keyframes flicker {
    0%,95%,100% { opacity: 1; }
    96% { opacity: 0.7; }
    97% { opacity: 1; }
    98% { opacity: 0.5; }
    99% { opacity: 1; }
  }

  .tagline {
    font-size: 15px;
    letter-spacing: 2px;
    margin: 16px 0 30px;
    color: var(--green-dim);
    min-height: 22px;
  }
  #typing-cursor::after {
    content: '█';
    animation: blink 1s step-end infinite;
  }
  @keyframes blink { 50% { opacity: 0; } }

  nav {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 6px;
    margin-top: 10px;
  }
  nav a {
    color: var(--green);
    text-decoration: none;
    font-size: 12px;
    letter-spacing: 2px;
    text-transform: uppercase;
    padding: 8px 18px;
    border: var(--border);
    border-radius: 2px;
    transition: all 0.2s;
    background: transparent;
  }
  nav a:hover {
    background: var(--green);
    color: #000;
    box-shadow: var(--green-glow);
    border-color: var(--green);
  }

  /* ── STATUS BAR ── */
  .status-bar {
    position: relative; z-index: 10;
    display: flex; gap: 20px; flex-wrap: wrap;
    justify-content: center;
    padding: 10px 20px;
    background: var(--bg2);
    border-bottom: var(--border);
    font-size: 11px;
    letter-spacing: 1px;
    color: #00ff9c99;
  }
  .status-dot {
    display: inline-block; width: 7px; height: 7px;
    background: var(--green); border-radius: 50%;
    margin-right: 6px;
    animation: pulse 2s ease-in-out infinite;
  }
  @keyframes pulse {
    0%,100% { opacity: 1; box-shadow: 0 0 4px var(--green); }
    50% { opacity: 0.4; box-shadow: none; }
  }

  /* ── SECTIONS ── */
  section {
    position: relative; z-index: 10;
    max-width: 960px;
    margin: 0 auto;
    padding: 80px 24px;
    border-bottom: var(--border);
  }

  .section-label {
    font-size: 10px;
    letter-spacing: 4px;
    color: #00ff9c66;
    text-transform: uppercase;
    margin-bottom: 6px;
  }

  h2 {
    font-family: 'Orbitron', sans-serif;
    font-size: clamp(20px, 3vw, 30px);
    font-weight: 700;
    letter-spacing: 4px;
    text-transform: uppercase;
    margin-bottom: 36px;
    display: flex; align-items: center; gap: 14px;
  }
  h2::after {
    content: '';
    flex: 1;
    height: 1px;
    background: linear-gradient(to right, #00ff9c55, transparent);
  }

  /* ── ABOUT ── */
  .about-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 24px;
  }
  @media (max-width: 600px) { .about-grid { grid-template-columns: 1fr; } }

  .about-card {
    background: var(--green-ghost);
    border: var(--border);
    padding: 24px;
    border-radius: 4px;
  }
  .about-card h3 {
    font-size: 11px; letter-spacing: 3px;
    text-transform: uppercase; color: var(--green-dim);
    margin-bottom: 12px;
  }
  .about-card p {
    font-size: 14px; line-height: 1.8; color: #aaffdd;
  }

  /* ── SKILLS ── */
  .skills-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 20px;
  }
  @media (max-width: 600px) { .skills-grid { grid-template-columns: 1fr; } }

  .skill-item { display: flex; flex-direction: column; gap: 8px; }
  .skill-header {
    display: flex; justify-content: space-between;
    font-size: 12px; letter-spacing: 2px;
    text-transform: uppercase;
  }
  .skill-pct { color: var(--green-dim); }
  .skill-track {
    height: 6px; background: #0d1f17;
    border-radius: 3px; overflow: hidden;
    border: 1px solid #00ff9c22;
  }
  .skill-fill {
    height: 100%; width: 0;
    background: linear-gradient(to right, #00cc7a, #00ff9c);
    border-radius: 3px;
    box-shadow: 0 0 8px #00ff9c88;
    transition: width 1.6s cubic-bezier(.22,1,.36,1);
  }

  /* ── PROJECTS ── */
  .projects-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 20px;
  }
  .project-card {
    border: var(--border);
    background: var(--green-ghost);
    padding: 28px;
    border-radius: 4px;
    position: relative;
    overflow: hidden;
    transition: transform 0.2s, box-shadow 0.2s;
  }
  .project-card:hover {
    transform: translateY(-4px);
    box-shadow: 0 8px 32px rgba(0,255,156,0.12);
    border-color: #00ff9c99;
  }
  .project-card::before {
    content: '';
    position: absolute; top: 0; left: 0;
    width: 3px; height: 100%;
    background: linear-gradient(to bottom, var(--green), transparent);
  }
  .project-tag {
    font-size: 10px; letter-spacing: 3px;
    text-transform: uppercase;
    color: var(--green-dim);
    margin-bottom: 10px;
  }
  .project-card h3 {
    font-family: 'Orbitron', sans-serif;
    font-size: 14px; letter-spacing: 2px;
    margin-bottom: 12px;
    text-transform: uppercase;
  }
  .project-card p { font-size: 13px; line-height: 1.8; color: #aaffdd; }
  .project-badge {
    display: inline-block; margin-top: 14px;
    font-size: 10px; letter-spacing: 2px;
    text-transform: uppercase;
    padding: 4px 12px;
    border: 1px solid #00ff9c44;
    border-radius: 2px;
    color: var(--green-dim);
  }

  /* ── CYBER LAB TERMINAL ── */
  .terminal-window {
    border: var(--border);
    border-radius: 6px;
    overflow: hidden;
    box-shadow: 0 0 40px rgba(0,255,156,0.08);
  }
  .terminal-bar {
    background: #0a1a12;
    padding: 10px 16px;
    display: flex; align-items: center; gap: 10px;
    border-bottom: var(--border);
    font-size: 11px; letter-spacing: 2px;
    color: #00ff9c88;
  }
  .t-dot {
    width: 11px; height: 11px; border-radius: 50%;
    display: inline-block;
  }
  .terminal-body {
    background: #020d07;
    padding: 28px;
    font-size: 13px;
    line-height: 2;
    min-height: 260px;
  }
  .t-line { display: flex; align-items: flex-start; gap: 10px; }
  .t-prompt { color: #00ff9c99; white-space: nowrap; flex-shrink: 0; }
  .t-cmd { color: var(--green); }
  .t-out { color: #aaffddbb; padding-left: 20px; }
  .t-highlight { color: var(--green); font-weight: bold; }
  .t-warn { color: #ffcc00; }
  .t-info { color: #00cfff; }

  /* ── CONTACT ── */
  .contact-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 16px;
  }
  @media (max-width: 500px) { .contact-grid { grid-template-columns: 1fr; } }

  .contact-item {
    display: flex; align-items: center; gap: 14px;
    background: var(--green-ghost);
    border: var(--border);
    padding: 18px 20px;
    border-radius: 4px;
    text-decoration: none;
    color: var(--green);
    font-size: 13px;
    letter-spacing: 1px;
    transition: all 0.2s;
  }
  .contact-item:hover {
    background: rgba(0,255,156,0.12);
    border-color: var(--green);
    box-shadow: var(--green-glow);
  }
  .contact-icon { font-size: 20px; }

  /* ── FOOTER ── */
  footer {
    position: relative; z-index: 10;
    text-align: center;
    padding: 30px;
    font-size: 11px;
    letter-spacing: 3px;
    color: #00ff9c44;
    text-transform: uppercase;
    border-top: var(--border);
  }
</style>
</head>
<body>

<canvas id="matrix"></canvas>

<!-- STATUS BAR -->
<div class="status-bar">
  <span><span class="status-dot"></span>SYSTEM ONLINE</span>
  <span>// SECURITY LEVEL: ALPHA</span>
  <span>// ISLAMABAD, PK</span>
  <span>// 🐺 CYBER WOLF CLUB</span>
  <span id="clock">00:00:00</span>
</div>

<!-- HEADER -->
<header>
  <h1 class="glitch" data-text="Abdullah Rashid">Abdullah Rashid</h1>
  <p class="tagline"><span id="typing-cursor"></span></p>
  <nav>
    <a href="#about">About</a>
    <a href="#skills">Skills</a>
    <a href="#projects">Projects</a>
    <a href="#lab">Cyber Lab</a>
    <a href="#contact">Contact</a>
  </nav>
</header>

<!-- ABOUT -->
<section id="about">
  <div class="section-label">// 01 — Profile</div>
  <h2>About Me</h2>
  <div class="about-grid">
    <div class="about-card">
      <h3>Who I Am</h3>
      <p>Cybersecurity enthusiast passionate about ethical hacking, penetration testing, and vulnerability research. I break systems to make them stronger.</p>
    </div>
    <div class="about-card">
      <h3>My Mission</h3>
      <p>Dedicated to identifying and mitigating real-world threats. Constantly learning, constantly pushing boundaries in the offensive security space.</p>
    </div>
    <div class="about-card">
      <h3>🐺 Community</h3>
      <p>Proud member of <strong>Cyber Wolf Club</strong> — a community of cybersecurity enthusiasts collaborating, learning, and hunting threats together.</p>
    </div>
    <div class="about-card">
      <h3>📍 Location</h3>
      <p>Based in <strong>Islamabad, Pakistan</strong>. Operating in the digital realm across borders — no firewall too strong.</p>
    </div>
  </div>
</section>

<!-- SKILLS -->
<section id="skills">
  <div class="section-label">// 02 — Arsenal</div>
  <h2>Skills</h2>
  <div class="skills-grid" id="skills-grid">
    <div class="skill-item">
      <div class="skill-header"><span>Kali Linux</span><span class="skill-pct">92%</span></div>
      <div class="skill-track"><div class="skill-fill" data-width="92"></div></div>
    </div>
    <div class="skill-item">
      <div class="skill-header"><span>Penetration Testing</span><span class="skill-pct">88%</span></div>
      <div class="skill-track"><div class="skill-fill" data-width="88"></div></div>
    </div>
    <div class="skill-item">
      <div class="skill-header"><span>Network Security</span><span class="skill-pct">85%</span></div>
      <div class="skill-track"><div class="skill-fill" data-width="85"></div></div>
    </div>
    <div class="skill-item">
      <div class="skill-header"><span>Nmap / Recon</span><span class="skill-pct">90%</span></div>
      <div class="skill-track"><div class="skill-fill" data-width="90"></div></div>
    </div>
    <div class="skill-item">
      <div class="skill-header"><span>Vulnerability Research</span><span class="skill-pct">80%</span></div>
      <div class="skill-track"><div class="skill-fill" data-width="80"></div></div>
    </div>
    <div class="skill-item">
      <div class="skill-header"><span>Linux / Bash</span><span class="skill-pct">87%</span></div>
      <div class="skill-track"><div class="skill-fill" data-width="87"></div></div>
    </div>
  </div>
</section>

<!-- PROJECTS -->
<section id="projects">
  <div class="section-label">// 03 — Operations</div>
  <h2>Projects</h2>
  <div class="projects-grid">
    <div class="project-card">
      <div class="project-tag">Operation 001</div>
      <h3>Kali Linux Bug Fix</h3>
      <p>Diagnosed and resolved a persistent terminal black screen and DBus permission issue in a Kali Linux environment. Root cause traced to misconfigured session bus.</p>
      <span class="project-badge">System Hardening</span>
    </div>
    <div class="project-card">
      <div class="project-tag">Operation 002</div>
      <h3>Network Recon Lab</h3>
      <p>Performed comprehensive vulnerability scanning using Nmap on an isolated lab network. Identified open ports, service versions, and OS fingerprints.</p>
      <span class="project-badge">Recon & OSINT</span>
    </div>
    <div class="project-card">
      <div class="project-tag">Operation 003</div>
      <h3>Home Lab Setup</h3>
      <p>Built a virtualized penetration testing environment using VirtualBox with segmented networks for safe offensive security practice and tool development.</p>
      <span class="project-badge">Lab Infrastructure</span>
    </div>
  </div>
</section>

<!-- CYBER LAB -->
<section id="lab">
  <div class="section-label">// 04 — Terminal</div>
  <h2>Cyber Lab</h2>
  <div class="terminal-window">
    <div class="terminal-bar">
      <span class="t-dot" style="background:#ff5f57"></span>
      <span class="t-dot" style="background:#febc2e"></span>
      <span class="t-dot" style="background:#28c840"></span>
      <span style="margin-left:10px;">root@kali:~$</span>
    </div>
    <div class="terminal-body">
      <div class="t-line"><span class="t-prompt">root@kali:~$</span><span class="t-cmd">sudo nmap -A -sV target.local</span></div>
      <div class="t-out t-warn">Starting Nmap 7.94 — https://nmap.org</div>
      <div class="t-out">Scanning target.local (192.168.1.105) ...</div>
      <div class="t-out t-highlight">PORT&nbsp;&nbsp;&nbsp; STATE SERVICE&nbsp; VERSION</div>
      <div class="t-out"><span class="t-info">22/tcp</span>&nbsp; open&nbsp; ssh&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; OpenSSH 9.2p1</div>
      <div class="t-out"><span class="t-info">80/tcp</span>&nbsp; open&nbsp; http&nbsp;&nbsp;&nbsp;&nbsp; Apache httpd 2.4.57</div>
      <div class="t-out"><span class="t-info">443/tcp</span> open&nbsp; ssl/https nginx 1.24.0</div>
      <div class="t-out t-warn">OS detection: Linux 5.x kernel</div>
      <div class="t-out t-highlight">Nmap done — 3 open ports identified.</div>
      <div class="t-line" style="margin-top:8px"><span class="t-prompt">root@kali:~$</span><span class="t-cmd" id="lab-cursor">█</span></div>
    </div>
  </div>
</section>

<!-- CONTACT -->
<section id="contact">
  <div class="section-label">// 05 — Comms</div>
  <h2>Contact</h2>
  <div class="contact-grid">
    <a class="contact-item" href="https://rashidabdullah5737-ai.github.io/" target="_blank">
      <span class="contact-icon">⌥</span>
      <span>rashidabdullah5737-ai.github.io</span>
    </a>
    <a class="contact-item" href="https://linkedin.com/in/abdullah-rashid-a1554b388" target="_blank">
      <span class="contact-icon">◈</span>
      <span>in/abdullah-rashid-a1554b388</span>
    </a>
    <a class="contact-item" href="mailto:rashidabdullah5737@gmail.com">
      <span class="contact-icon">✉</span>
      <span>rashidabdullah5737@gmail.com</span>
    </a>
    <div class="contact-item" style="cursor:default;">
      <span class="contact-icon">🐺</span>
      <span>Cyber Wolf Club — Member</span>
    </div>
  </div>
</section>

<footer>
  <p>© 2026 Abdullah Rashid — Ethical Hacker | All Rights Reserved</p>
</footer>

<script>
/* ── CLOCK ── */
function updateClock() {
  const now = new Date();
  const h = String(now.getHours()).padStart(2,'0');
  const m = String(now.getMinutes()).padStart(2,'0');
  const s = String(now.getSeconds()).padStart(2,'0');
  document.getElementById('clock').textContent = h+':'+m+':'+s;
}
setInterval(updateClock, 1000); updateClock();

/* ── TYPING ── */
const phrases = [
  'Ethical Hacker',
  'Penetration Tester',
  'Cybersecurity Researcher',
  'Kali Linux Enthusiast'
];
let pi = 0, ci = 0, deleting = false;
const el = document.getElementById('typing-cursor');
function typeLoop() {
  const word = phrases[pi];
  if (!deleting) {
    el.textContent = word.slice(0, ++ci);
    if (ci === word.length) { deleting = true; setTimeout(typeLoop, 1800); return; }
  } else {
    el.textContent = word.slice(0, --ci);
    if (ci === 0) { deleting = false; pi = (pi+1) % phrases.length; }
  }
  setTimeout(typeLoop, deleting ? 40 : 85);
}
typeLoop();

/* ── MATRIX ── */
const canvas = document.getElementById('matrix');
const ctx = canvas.getContext('2d');
function resizeCanvas() {
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
}
resizeCanvas();
window.addEventListener('resize', resizeCanvas);

const chars = '01アイウエオカキクケコサシスセソタチツテトナニヌネノ';
const fontSize = 13;
let drops = [];
function initDrops() {
  const cols = Math.floor(canvas.width / fontSize);
  drops = Array.from({length: cols}, () => Math.random() * -100);
}
initDrops();
window.addEventListener('resize', initDrops);

function drawMatrix() {
  ctx.fillStyle = 'rgba(0,0,0,0.05)';
  ctx.fillRect(0, 0, canvas.width, canvas.height);
  ctx.fillStyle = '#00ff9c';
  ctx.font = fontSize + 'px Share Tech Mono';
  drops.forEach((y, i) => {
    const char = chars[Math.floor(Math.random() * chars.length)];
    ctx.globalAlpha = Math.random() * 0.5 + 0.3;
    ctx.fillText(char, i * fontSize, y * fontSize);
    ctx.globalAlpha = 1;
    if (y * fontSize > canvas.height && Math.random() > 0.975) drops[i] = 0;
    drops[i] += 0.5;
  });
}
setInterval(drawMatrix, 40);

/* ── SKILL BARS (IntersectionObserver) ── */
const fills = document.querySelectorAll('.skill-fill');
const obs = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      e.target.style.width = e.target.dataset.width + '%';
      obs.unobserve(e.target);
    }
  });
}, { threshold: 0.3 });
fills.forEach(f => obs.observe(f));

/* ── LAB CURSOR BLINK ── */
setInterval(() => {
  const c = document.getElementById('lab-cursor');
  if (c) c.style.opacity = c.style.opacity === '0' ? '1' : '0';
}, 600);
</script>
</body>
</html>
