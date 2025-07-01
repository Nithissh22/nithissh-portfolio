<!DOCTYPE html>
<html lang="en" data-theme="dark">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1.0"/>
  <title>Nithissh | Futuristic Portfolio</title>
  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Google Fonts -->
  <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@700&family=Inter:wght@400;700&display=swap" rel="stylesheet">
  <!-- Font Awesome for icons -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.2/css/all.min.css"/>
  <style>
    html {
      scroll-behavior: smooth;
    }
    body {
      font-family: 'Inter', Arial, sans-serif;
      background: var(--bg-gradient);
      transition: background 0.5s;
    }
    [data-theme="dark"] {
      --bg-gradient: linear-gradient(135deg, #0f2027 0%, #2c5364 100%);
      --neon: #00ffe7;
      --neon-glow: 0 0 12px #00ffe7, 0 0 24px #00ffe788;
      --text: #e0e0e0;
      --card: #1a2636cc;
    }
    [data-theme="light"] {
      --bg-gradient: linear-gradient(135deg, #f8fafc 0%, #e0e7ef 100%);
      --neon: #007cf0;
      --neon-glow: 0 0 12px #007cf0, 0 0 24px #007cf088;
      --text: #222;
      --card: #fff9;
    }
    [data-theme="cosmic"] {
      --bg-gradient: radial-gradient(ellipse at 60% 40%, #2e026d 0%, #0f2027 100%);
      --neon: #ff00ea;
      --neon-glow: 0 0 16px #ff00ea, 0 0 32px #ff00ea88;
      --text: #f5eaff;
      --card: #2e026dcc;
    }
    .neon-border {
      border: 4px solid var(--neon);
      box-shadow: var(--neon-glow);
      transition: box-shadow 0.3s, border-color 0.3s;
    }
    .neon-border:hover {
      animation: pulse 1s infinite alternate;
    }
    @keyframes pulse {
      0% { box-shadow: var(--neon-glow); }
      100% { box-shadow: 0 0 32px 8px var(--neon), 0 0 64px 16px var(--neon); }
    }
    .particle-bg {
      position: absolute;
      inset: 0;
      z-index: 0;
      pointer-events: none;
    }
    .timeline-dot {
      box-shadow: 0 0 8px 2px var(--neon);
      background: var(--neon);
    }
    .timeline-card {
      background: var(--card);
      border-left: 4px solid var(--neon);
      transition: transform 0.4s cubic-bezier(.4,2,.6,1), box-shadow 0.3s;
    }
    .timeline-card.visible {
      transform: translateX(0);
      box-shadow: 0 4px 32px -8px var(--neon);
    }
    .timeline-card {
      transform: translateX(-60px);
      opacity: 0.7;
    }
    .timeline-card.visible {
      opacity: 1;
    }
    .radar-chart {
      width: 320px;
      height: 320px;
      margin: auto;
      display: block;
    }
    .mindmap-node {
      background: var(--card);
      border: 2px solid var(--neon);
      box-shadow: 0 0 8px var(--neon);
      transition: transform 0.2s, box-shadow 0.2s;
    }
    .mindmap-node:hover {
      transform: scale(1.08) rotate(-2deg);
      box-shadow: 0 0 24px 4px var(--neon);
    }
    .theme-btn.active {
      border-color: var(--neon);
      box-shadow: 0 0 8px var(--neon);
    }
    .microinteraction {
      transition: transform 0.15s, box-shadow 0.15s;
    }
    .microinteraction:hover {
      transform: translateY(-2px) scale(1.04);
      box-shadow: 0 2px 12px -2px var(--neon);
    }
    .chatbot-bubble {
      background: var(--card);
      color: var(--text);
      border-radius: 1.2em;
      padding: 0.7em 1.2em;
      margin: 0.3em 0;
      max-width: 80%;
      box-shadow: 0 2px 12px -2px var(--neon);
      font-size: 1em;
    }
    .chatbot-bubble.user {
      align-self: flex-end;
      background: var(--neon);
      color: #222;
    }
    .chatbot-bubble.bot {
      align-self: flex-start;
    }
    .back-to-top {
      position: fixed;
      right: 2vw;
      bottom: 2vw;
      z-index: 50;
      background: var(--neon);
      color: #111;
      border-radius: 50%;
      width: 48px;
      height: 48px;
      display: flex;
      align-items: center;
      justify-content: center;
      box-shadow: var(--neon-glow);
      cursor: pointer;
      opacity: 0.8;
      transition: opacity 0.2s;
    }
    .back-to-top:hover {
      opacity: 1;
    }
    /* Hide scrollbars for particle bg */
    ::-webkit-scrollbar { width: 8px; background: transparent; }
    ::-webkit-scrollbar-thumb { background: var(--neon); border-radius: 8px; }
  </style>
</head>
<body class="relative min-h-screen text-base" style="color:var(--text)">
  <!-- Particle Background -->
  <canvas id="particle-bg" class="particle-bg"></canvas>

  <!-- Header / Hero Section -->
  <header class="relative z-10 flex flex-col items-center justify-center min-h-screen text-center px-4">
    <div class="mt-24 mb-8">
      <div class="inline-block neon-border rounded-full p-2 transition-all duration-300" style="box-shadow: var(--neon-glow);">
        <img src="https://avatars.githubusercontent.com/u/9919?v=4" alt="Profile Photo" width="160" height="160"
          class="rounded-full object-cover transition-all duration-300" id="profile-photo" loading="lazy"/>
      </div>
    </div>
    <h1 class="text-4xl md:text-6xl font-orbitron font-bold mb-4" style="font-family:'Orbitron',sans-serif;letter-spacing:0.04em;">
      Nithissh <span class="text-[var(--neon)]">Portfolio</span>
    </h1>
    <p class="max-w-xl mx-auto text-lg md:text-2xl mb-8" style="color:var(--text)">
      🚀 Building the future, one pixel at a time. <span class="text-[var(--neon)]">AI, code, and cosmic creativity.</span>
    </p>
    <div class="flex flex-wrap gap-4 justify-center mb-8">
      <button class="theme-btn px-4 py-2 rounded-lg border-2 border-transparent microinteraction" data-theme="light">
        ☀️ Light
      </button>
      <button class="theme-btn px-4 py-2 rounded-lg border-2 border-transparent microinteraction" data-theme="dark">
        🌙 Dark
      </button>
      <button class="theme-btn px-4 py-2 rounded-lg border-2 border-transparent microinteraction" data-theme="cosmic">
        🪐 Cosmic
      </button>
      <button id="voice-btn" class="px-4 py-2 rounded-lg border-2 border-[var(--neon)] microinteraction" title="Voice Command">
        <i class="fa fa-microphone"></i> Voice
      </button>
      <a href="#contact" class="px-4 py-2 rounded-lg border-2 border-[var(--neon)] microinteraction" style="color:var(--neon)">
        Contact
      </a>
      <a href="resume.pdf" download class="px-4 py-2 rounded-lg border-2 border-[var(--neon)] microinteraction" style="color:var(--neon)">
        <i class="fa fa-download"></i> Resume
      </a>
    </div>
    <div class="flex justify-center mt-4">
      <div class="flex items-center gap-4">
        <a href="https://github.com/" target="_blank" class="text-2xl microinteraction" style="color:var(--neon)"><i class="fab fa-github"></i></a>
        <a href="https://linkedin.com/" target="_blank" class="text-2xl microinteraction" style="color:var(--neon)"><i class="fab fa-linkedin"></i></a>
        <a href="mailto:youremail@example.com" class="text-2xl microinteraction" style="color:var(--neon)"><i class="fa fa-envelope"></i></a>
      </div>
    </div>
    <div class="mt-16 animate-bounce">
      <a href="#timeline" class="text-[var(--neon)] text-3xl"><i class="fa fa-chevron-down"></i></a>
    </div>
  </header>

  <!-- AI Chatbot Section -->
  <section id="chatbot" class="relative z-10 max-w-xl mx-auto my-16 p-6 rounded-2xl shadow-lg" style="background:var(--card)">
    <h2 class="text-2xl font-bold mb-2" style="color:var(--neon)">🤖 AI Chatbot</h2>
    <div id="chatbot-window" class="flex flex-col gap-2 h-48 overflow-y-auto mb-2"></div>
    <form id="chatbot-form" class="flex gap-2">
      <input type="text" id="chatbot-input" class="flex-1 rounded-lg px-3 py-2 bg-transparent border border-[var(--neon)] focus:outline-none" placeholder="Ask me anything..." autocomplete="off"/>
      <button type="submit" class="px-4 py-2 rounded-lg border-2 border-[var(--neon)] microinteraction" style="color:var(--neon)">Send</button>
    </form>
    <div class="text-xs mt-1 text-right text-[var(--neon)]">AI is <b>mocked</b> for demo</div>
  </section>

  <!-- Timeline Section -->
  <section id="timeline" class="relative z-10 max-w-3xl mx-auto my-20 px-4">
    <h2 class="text-3xl font-bold mb-8 text-center" style="color:var(--neon)">🚀 My Journey</h2>
    <div class="relative pl-8">
      <div class="absolute left-2 top-0 bottom-0 w-1 bg-gradient-to-b from-[var(--neon)] to-transparent"></div>
      <div id="timeline-list" class="flex flex-col gap-10">
        <!-- Timeline items will be injected by JS -->
      </div>
    </div>
  </section>

  <!-- Skills Radar Chart -->
  <section id="skills" class="relative z-10 max-w-2xl mx-auto my-20 px-4">
    <h2 class="text-3xl font-bold mb-8 text-center" style="color:var(--neon)">🛠️ Skills</h2>
    <canvas id="radar-chart" class="radar-chart"></canvas>
    <div class="flex flex-wrap justify-center gap-4 mt-6">
      <span class="px-3 py-1 rounded-lg microinteraction" style="background:var(--card);color:var(--neon)">JavaScript</span>
      <span class="px-3 py-1 rounded-lg microinteraction" style="background:var(--card);color:var(--neon)">React</span>
      <span class="px-3 py-1 rounded-lg microinteraction" style="background:var(--card);color:var(--neon)">AI/ML</span>
      <span class="px-3 py-1 rounded-lg microinteraction" style="background:var(--card);color:var(--neon)">UI/UX</span>
      <span class="px-3 py-1 rounded-lg microinteraction" style="background:var(--card);color:var(--neon)">Node.js</span>
      <span class="px-3 py-1 rounded-lg microinteraction" style="background:var(--card);color:var(--neon)">Cloud</span>
    </div>
  </section>

  <!-- My Universe Mindmap -->
  <section id="universe" class="relative z-10 max-w-5xl mx-auto my-20 px-4">
    <h2 class="text-3xl font-bold mb-8 text-center" style="color:var(--neon)">🌌 My Universe</h2>
    <div id="mindmap" class="relative w-full h-[420px] mx-auto"></div>
  </section>

  <!-- Contact Section -->
  <section id="contact" class="relative z-10 max-w-xl mx-auto my-20 px-4">
    <h2 class="text-3xl font-bold mb-8 text-center" style="color:var(--neon)">📬 Contact Me</h2>
    <form id="contact-form" class="flex flex-col gap-4 bg-[var(--card)] p-6 rounded-2xl shadow-lg">
      <input type="text" name="name" required placeholder="Your Name" class="rounded-lg px-3 py-2 bg-transparent border border-[var(--neon)] focus:outline-none"/>
      <input type="email" name="email" required placeholder="Your Email" class="rounded-lg px-3 py-2 bg-transparent border border-[var(--neon)] focus:outline-none"/>
      <textarea name="message" required placeholder="Your Message" rows="4" class="rounded-lg px-3 py-2 bg-transparent border border-[var(--neon)] focus:outline-none"></textarea>
      <button type="submit" class="px-4 py-2 rounded-lg border-2 border-[var(--neon)] microinteraction" style="color:var(--neon)">Send</button>
    </form>
    <div id="contact-success" class="hidden mt-4 text-center text-[var(--neon)] font-bold">Thank you! I'll get back to you soon.</div>
  </section>

  <!-- Back to Top Button -->
  <div id="back-to-top" class="back-to-top" title="Back to top" style="display:none;">
    <i class="fa fa-arrow-up"></i>
  </div>

  <!-- JavaScript Section -->
  <script>
    // --- Particle Background ---
    // Simple interactive particles using canvas
    const canvas = document.getElementById('particle-bg');
    const ctx = canvas.getContext('2d');
    let particles = [];
    const PARTICLE_COUNT = 80;
    function resizeCanvas() {
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    }
    window.addEventListener('resize', resizeCanvas);
    function createParticles() {
      particles = [];
      for (let i = 0; i < PARTICLE_COUNT; i++) {
        particles.push({
          x: Math.random() * canvas.width,
          y: Math.random() * canvas.height,
          vx: (Math.random() - 0.5) * 1.2,
          vy: (Math.random() - 0.5) * 1.2,
          r: Math.random() * 2.2 + 1.2
        });
      }
    }
    function drawParticles() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      for (let p of particles) {
        ctx.beginPath();
        ctx.arc(p.x, p.y, p.r, 0, 2 * Math.PI);
        ctx.fillStyle = getComputedStyle(document.documentElement).getPropertyValue('--neon');
        ctx.shadowColor = ctx.fillStyle;
        ctx.shadowBlur = 12;
        ctx.fill();
      }
      // Draw lines between close particles
      for (let i = 0; i < particles.length; i++) {
        for (let j = i + 1; j < particles.length; j++) {
          let a = particles[i], b = particles[j];
          let dist = Math.hypot(a.x - b.x, a.y - b.y);
          if (dist < 100) {
            ctx.beginPath();
            ctx.moveTo(a.x, a.y);
            ctx.lineTo(b.x, b.y);
            ctx.strokeStyle = getComputedStyle(document.documentElement).getPropertyValue('--neon') + '88';
            ctx.lineWidth = 0.7;
            ctx.stroke();
          }
        }
      }
    }
    function updateParticles() {
      for (let p of particles) {
        p.x += p.vx;
        p.y += p.vy;
        if (p.x < 0 || p.x > canvas.width) p.vx *= -1;
        if (p.y < 0 || p.y > canvas.height) p.vy *= -1;
      }
    }
    function animateParticles() {
      updateParticles();
      drawParticles();
      requestAnimationFrame(animateParticles);
    }
    function interactParticles(e) {
      let mx = e.clientX, my = e.clientY;
      for (let p of particles) {
        let dist = Math.hypot(p.x - mx, p.y - my);
        if (dist < 80) {
          let angle = Math.atan2(p.y - my, p.x - mx);
          p.vx += Math.cos(angle) * 0.05;
          p.vy += Math.sin(angle) * 0.05;
        }
      }
    }
    resizeCanvas();
    createParticles();
    animateParticles();
    window.addEventListener('mousemove', interactParticles);

    // --- Theme Changer ---
    const themeBtns = document.querySelectorAll('.theme-btn');
    function setTheme(theme) {
      document.documentElement.setAttribute('data-theme', theme);
      themeBtns.forEach(btn => btn.classList.toggle('active', btn.dataset.theme === theme));
    }
    themeBtns.forEach(btn => {
      btn.addEventListener('click', () => setTheme(btn.dataset.theme));
    });
    // Default theme
    setTheme('dark');

    // --- Voice Command (Web Speech API) ---
    const voiceBtn = document.getElementById('voice-btn');
    let recognizing = false;
    let recognition;
    if ('webkitSpeechRecognition' in window || 'SpeechRecognition' in window) {
      const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
      recognition = new SpeechRecognition();
      recognition.lang = 'en-US';
      recognition.continuous = false;
      recognition.interimResults = false;
      recognition.onresult = function(event) {
        const command = event.results[0][0].transcript.toLowerCase();
        handleVoiceCommand(command);
      };
      recognition.onend = () => { recognizing = false; voiceBtn.innerHTML = '<i class="fa fa-microphone"></i> Voice'; };
      voiceBtn.addEventListener('click', () => {
        if (!recognizing) {
          recognition.start();
          recognizing = true;
          voiceBtn.innerHTML = '<i class="fa fa-wave-square"></i> Listening...';
        } else {
          recognition.stop();
        }
      });
    } else {
      voiceBtn.disabled = true;
      voiceBtn.title = "Voice not supported";
    }
    function handleVoiceCommand(cmd) {
      if (cmd.includes('light')) setTheme('light');
      else if (cmd.includes('dark')) setTheme('dark');
      else if (cmd.includes('cosmic')) setTheme('cosmic');
      else if (cmd.includes('top')) window.scrollTo({top:0,behavior:'smooth'});
      else if (cmd.includes('contact')) document.getElementById('contact').scrollIntoView({behavior:'smooth'});
      else if (cmd.includes('timeline') || cmd.includes('journey')) document.getElementById('timeline').scrollIntoView({behavior:'smooth'});
      else if (cmd.includes('skills')) document.getElementById('skills').scrollIntoView({behavior:'smooth'});
      else if (cmd.includes('universe')) document.getElementById('universe').scrollIntoView({behavior:'smooth'});
      else alert('Voice command not recognized: ' + cmd);
    }

    // --- Back to Top Button ---
    const backToTop = document.getElementById('back-to-top');
    window.addEventListener('scroll', () => {
      backToTop.style.display = window.scrollY > 400 ? 'flex' : 'none';
    });
    backToTop.addEventListener('click', () => {
      window.scrollTo({top:0,behavior:'smooth'});
    });

    // --- Timeline with Scroll Animations ---
    const timelineData = [
      {
        year: '2024',
        title: 'Launched Futuristic Portfolio',
        desc: 'Built a next-level, AI-powered portfolio with cosmic vibes and interactive features.',
        icon: 'fa-rocket'
      },
      {
        year: '2023',
        title: 'AI/ML Research Intern',
        desc: 'Worked on generative AI models and deployed smart web apps.',
        icon: 'fa-brain'
      },
      {
        year: '2022',
        title: 'Fullstack Developer',
        desc: 'Developed scalable apps using React, Node.js, and cloud services.',
        icon: 'fa-code'
      },
      {
        year: '2021',
        title: 'UI/UX Designer',
        desc: 'Crafted delightful user experiences and futuristic interfaces.',
        icon: 'fa-palette'
      },
      {
        year: '2020',
        title: 'Started My Journey',
        desc: 'Began my adventure in tech, learning and building every day.',
        icon: 'fa-seedling'
      }
    ];
    const timelineList = document.getElementById('timeline-list');
    timelineData.forEach((item, idx) => {
      const card = document.createElement('div');
      card.className = 'timeline-card p-6 rounded-xl shadow-lg flex items-start gap-4';
      card.innerHTML = `
        <div class="timeline-dot w-6 h-6 rounded-full flex items-center justify-center mt-1">
          <i class="fa ${item.icon} text-white"></i>
        </div>
        <div>
          <div class="text-lg font-bold" style="color:var(--neon)">${item.year} — ${item.title}</div>
          <div class="text-base" style="color:var(--text)">${item.desc}</div>
        </div>
      `;
      timelineList.appendChild(card);
    });
    // Scroll animation
    function revealTimeline() {
      const cards = document.querySelectorAll('.timeline-card');
      const trigger = window.innerHeight * 0.85;
      cards.forEach(card => {
        const rect = card.getBoundingClientRect();
        if (rect.top < trigger) card.classList.add('visible');
        else card.classList.remove('visible');
      });
    }
    window.addEventListener('scroll', revealTimeline);
    revealTimeline();

    // --- Animated Radar Chart (Skills) ---
    // Custom radar chart using canvas
    const radar = document.getElementById('radar-chart');
    const radarCtx = radar.getContext('2d');
    const radarLabels = ['JavaScript','React','AI/ML','UI/UX','Node.js','Cloud'];
    const radarData = [90, 85, 80, 75, 70, 65]; // out of 100
    function drawRadarChart(anim=1) {
      radarCtx.clearRect(0,0,radar.width,radar.height);
      const cx = radar.width/2, cy = radar.height/2, r = 110;
      // Draw web
      for (let level=1; level<=5; level++) {
        radarCtx.beginPath();
        for (let i=0; i<6; i++) {
          let angle = Math.PI/3*i-Math.PI/2;
          let x = cx + Math.cos(angle)*r*level/5;
          let y = cy + Math.sin(angle)*r*level/5;
          if (i===0) radarCtx.moveTo(x,y);
          else radarCtx.lineTo(x,y);
        }
        radarCtx.closePath();
        radarCtx.strokeStyle = 'rgba(0,255,255,0.15)';
        radarCtx.stroke();
      }
      // Draw axes
      for (let i=0; i<6; i++) {
        let angle = Math.PI/3*i-Math.PI/2;
        radarCtx.beginPath();
        radarCtx.moveTo(cx,cy);
        radarCtx.lineTo(cx+Math.cos(angle)*r, cy+Math.sin(angle)*r);
        radarCtx.strokeStyle = 'rgba(0,255,255,0.18)';
        radarCtx.stroke();
        // Label
        radarCtx.save();
        radarCtx.translate(cx+Math.cos(angle)*(r+24), cy+Math.sin(angle)*(r+24));
        radarCtx.rotate(angle);
        radarCtx.font = 'bold 1em Inter';
        radarCtx.fillStyle = getComputedStyle(document.documentElement).getPropertyValue('--neon');
        radarCtx.textAlign = 'center';
        radarCtx.fillText(radarLabels[i],0,0);
        radarCtx.restore();
      }
      // Draw data
      radarCtx.beginPath();
      for (let i=0; i<6; i++) {
        let angle = Math.PI/3*i-Math.PI/2;
        let value = radarData[i]*anim/100;
        let x = cx + Math.cos(angle)*r*value;
        let y = cy + Math.sin(angle)*r*value;
        if (i===0) radarCtx.moveTo(x,y);
        else radarCtx.lineTo(x,y);
      }
      radarCtx.closePath();
      radarCtx.strokeStyle = getComputedStyle(document.documentElement).getPropertyValue('--neon');
      radarCtx.lineWidth = 3;
      radarCtx.shadowColor = getComputedStyle(document.documentElement).getPropertyValue('--neon');
      radarCtx.shadowBlur = 12;
      radarCtx.stroke();
      radarCtx.shadowBlur = 0;
      // Dots
      for (let i=0; i<6; i++) {
        let angle = Math.PI/3*i-Math.PI/2;
        let value = radarData[i]*anim/100;
        let x = cx + Math.cos(angle)*r*value;
        let y = cy + Math.sin(angle)*r*value;
        radarCtx.beginPath();
        radarCtx.arc(x,y,7,0,2*Math.PI);
        radarCtx.fillStyle = getComputedStyle(document.documentElement).getPropertyValue('--neon');
        radarCtx.shadowColor = getComputedStyle(document.documentElement).getPropertyValue('--neon');
        radarCtx.shadowBlur = 8;
        radarCtx.fill();
        radarCtx.shadowBlur = 0;
      }
    }
    // Animate radar chart on scroll into view
    function animateRadar() {
      const rect = radar.getBoundingClientRect();
      if (rect.top < window.innerHeight*0.8) {
        let t = 0;
        function anim() {
          t += 0.04;
          drawRadarChart(Math.min(1, t));
          if (t < 1) requestAnimationFrame(anim);
        }
        anim();
        window.removeEventListener('scroll', animateRadar);
      }
    }
    window.addEventListener('scroll', animateRadar);
    drawRadarChart(0.1);

    // --- Mindmap ("My Universe") ---
    // Simple force-directed mindmap
    const mindmapData = {
      name: "Me",
      children: [
        { name: "Interests", children: [
          { name: "AI" }, { name: "Space" }, { name: "Music" }, { name: "Gaming" }
        ]},
        { name: "Tools", children: [
          { name: "VS Code" }, { name: "GitHub" }, { name: "Figma" }, { name: "Notion" }
        ]},
        { name: "Dream Goals", children: [
          { name: "Build an AI startup" }, { name: "Travel to Mars" }, { name: "Write a book" }
        ]}
      ]
    };
    const mindmap = document.getElementById('mindmap');
    // Node positions
    let nodes = [];
    let links = [];
    function buildMindmapData() {
      nodes = [];
      links = [];
      let id = 0;
      function traverse(node, parent=null, depth=0, angle=0) {
        node.id = id++;
        node.depth = depth;
        node.angle = angle;
        nodes.push(node);
        if (parent) links.push({source: parent.id, target: node.id});
        if (node.children) {
          let step = Math.PI*2/node.children.length;
          node.children.forEach((child, i) => {
            traverse(child, node, depth+1, angle + i*step);
          });
        }
      }
      traverse(mindmapData);
    }
    function renderMindmap() {
      mindmap.innerHTML = '';
      const w = mindmap.offsetWidth, h = mindmap.offsetHeight;
      // Calculate positions
      nodes.forEach(node => {
        if (node.depth === 0) {
          node.x = w/2; node.y = h/2;
        } else {
          let r = 80 + node.depth*70;
          node.x = w/2 + Math.cos(node.angle)*r;
          node.y = h/2 + Math.sin(node.angle)*r;
        }
      });
      // Draw links
      links.forEach(link => {
        const s = nodes[link.source], t = nodes[link.target];
        const line = document.createElement('div');
        line.style.position = 'absolute';
        line.style.left = Math.min(s.x, t.x) + 'px';
        line.style.top = Math.min(s.y, t.y) + 'px';
        line.style.width = Math.abs(s.x - t.x) + 'px';
        line.style.height = Math.abs(s.y - t.y) + 'px';
        line.style.pointerEvents = 'none';
        line.innerHTML = `<svg width="${Math.abs(s.x-t.x)}" height="${Math.abs(s.y-t.y)}" style="overflow:visible">
          <line x1="${s.x<t.x?0:Math.abs(s.x-t.x)}" y1="${s.y<t.y?0:Math.abs(s.y-t.y)}"
                x2="${s.x>t.x?0:Math.abs(s.x-t.x)}" y2="${s.y>t.y?0:Math.abs(s.y-t.y)}"
                stroke="${getComputedStyle(document.documentElement).getPropertyValue('--neon')}" stroke-width="2" stroke-opacity="0.5"/>
        </svg>`;
        mindmap.appendChild(line);
      });
      // Draw nodes
      nodes.forEach(node => {
        const div = document.createElement('div');
        div.className = 'mindmap-node absolute px-4 py-2 rounded-xl text-center font-bold microinteraction';
        div.style.left = (node.x-48) + 'px';
        div.style.top = (node.y-24) + 'px';
        div.style.minWidth = '80px';
        div.style.zIndex = 2 + node.depth;
        div.innerText = node.name;
        mindmap.appendChild(div);
      });
    }
    buildMindmapData();
    renderMindmap();
    window.addEventListener('resize', renderMindmap);

    // --- AI Chatbot (Mocked) ---
    const chatbotWindow = document.getElementById('chatbot-window');
    const chatbotForm = document.getElementById('chatbot-form');
    const chatbotInput = document.getElementById('chatbot-input');
    function addChatBubble(text, sender='bot') {
      const div = document.createElement('div');
      div.className = 'chatbot-bubble ' + sender;
      div.innerText = text;
      chatbotWindow.appendChild(div);
      chatbotWindow.scrollTop = chatbotWindow.scrollHeight;
    }
    // Simple mock AI responses
    function getAIResponse(msg) {
      msg = msg.toLowerCase();
      if (msg.includes('name')) return "I'm Nithissh's AI assistant. Ask me anything!";
      if (msg.includes('skills')) return "JavaScript, React, AI/ML, UI/UX, Node.js, Cloud, and more!";
      if (msg.includes('contact')) return "You can use the contact form below or email directly.";
      if (msg.includes('theme')) return "Try switching themes with the buttons or say 'cosmic mode'!";
      if (msg.includes('resume')) return "Click the Resume button above to download it.";
      if (msg.includes('project')) return "Check out the timeline for my latest projects!";
      return "I'm here to help! Ask me about my skills, projects, or how to use this site.";
    }
    chatbotForm.addEventListener('submit', e => {
      e.preventDefault();
      const msg = chatbotInput.value.trim();
      if (!msg) return;
      addChatBubble(msg, 'user');
      setTimeout(() => {
        addChatBubble(getAIResponse(msg), 'bot');
      }, 600);
      chatbotInput.value = '';
    });

    // --- Contact Form (Mocked) ---
    const contactForm = document.getElementById('contact-form');
    const contactSuccess = document.getElementById('contact-success');
    contactForm.addEventListener('submit', e => {
      e.preventDefault();
      contactForm.style.display = 'none';
      contactSuccess.style.display = 'block';
    });

    // --- Lazy Load Images ---
    // (Profile photo already uses loading="lazy")

    // --- Neon Border Animation on Hover (Profile Photo) ---
    // (Handled by CSS)

    // --- Smooth Transitions & Microinteractions ---
    // (Handled by CSS)

    // --- Resume Download ---
    // (Handled by <a download>)

    // --- Responsive Design ---
    // (Tailwind + CSS)

    // --- Subtle Hover Microinteractions ---
    // (Handled by .microinteraction class)

    // --- Dynamic Theme on Mindmap and Radar Chart ---
    function updateDynamicVisuals() {
      drawRadarChart(1);
      renderMindmap();
    }
    const observer = new MutationObserver(updateDynamicVisuals);
    observer.observe(document.documentElement, { attributes: true, attributeFilter: ['data-theme'] });

    // --- End of Script ---
  </script>
</body>
</html>
