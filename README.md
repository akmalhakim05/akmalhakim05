<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Akmal Hakim – Backend Developer</title>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@300;400;700;800&family=Syne:wght@400;700;800&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #060810;
    --surface: #0d1117;
    --surface2: #161b22;
    --accent: #00d4ff;
    --accent2: #ff6b35;
    --accent3: #7fff6e;
    --text: #e6edf3;
    --muted: #8b949e;
    --border: #21262d;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'JetBrains Mono', monospace;
    overflow-x: hidden;
    cursor: none;
  }

  /* Custom cursor */
  .cursor {
    position: fixed;
    width: 12px; height: 12px;
    background: var(--accent);
    border-radius: 50%;
    pointer-events: none;
    z-index: 9999;
    transform: translate(-50%, -50%);
    transition: transform 0.1s, background 0.2s;
    mix-blend-mode: screen;
  }
  .cursor-trail {
    position: fixed;
    width: 32px; height: 32px;
    border: 1px solid var(--accent);
    border-radius: 50%;
    pointer-events: none;
    z-index: 9998;
    transform: translate(-50%, -50%);
    transition: left 0.15s ease, top 0.15s ease, opacity 0.3s;
    opacity: 0.4;
  }

  /* Grid background */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image:
      linear-gradient(rgba(0,212,255,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,212,255,0.03) 1px, transparent 1px);
    background-size: 40px 40px;
    pointer-events: none;
    z-index: 0;
  }

  /* Floating particles */
  .particles {
    position: fixed;
    inset: 0;
    pointer-events: none;
    z-index: 1;
  }
  .particle {
    position: absolute;
    width: 2px; height: 2px;
    background: var(--accent);
    border-radius: 50%;
    animation: float-up linear infinite;
    opacity: 0;
  }
  @keyframes float-up {
    0% { transform: translateY(100vh) translateX(0); opacity: 0; }
    10% { opacity: 0.6; }
    90% { opacity: 0.3; }
    100% { transform: translateY(-20px) translateX(40px); opacity: 0; }
  }

  /* Main layout */
  .container {
    max-width: 900px;
    margin: 0 auto;
    padding: 60px 24px 100px;
    position: relative;
    z-index: 10;
  }

  /* Hero section */
  .hero {
    text-align: center;
    padding: 80px 0 60px;
    position: relative;
  }

  .status-bar {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    background: rgba(0,212,255,0.08);
    border: 1px solid rgba(0,212,255,0.2);
    padding: 6px 16px;
    border-radius: 100px;
    font-size: 12px;
    color: var(--accent);
    margin-bottom: 32px;
    animation: fadeSlideDown 0.8s ease forwards;
    opacity: 0;
    letter-spacing: 0.1em;
  }
  .status-dot {
    width: 6px; height: 6px;
    background: var(--accent3);
    border-radius: 50%;
    animation: pulse 2s ease infinite;
  }
  @keyframes pulse {
    0%, 100% { opacity: 1; box-shadow: 0 0 0 0 rgba(127,255,110,0.4); }
    50% { opacity: 0.7; box-shadow: 0 0 0 6px rgba(127,255,110,0); }
  }

  .hero-name {
    font-family: 'Syne', sans-serif;
    font-size: clamp(52px, 10vw, 96px);
    font-weight: 800;
    line-height: 0.95;
    letter-spacing: -0.03em;
    margin-bottom: 16px;
    opacity: 0;
    animation: fadeSlideUp 0.9s 0.2s ease forwards;
  }
  .hero-name span {
    display: block;
    background: linear-gradient(135deg, var(--accent) 0%, #0099ff 50%, var(--accent2) 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    animation: shimmer 4s linear infinite;
    background-size: 200% auto;
  }
  @keyframes shimmer {
    0% { background-position: 0% center; }
    100% { background-position: 200% center; }
  }

  .hero-title {
    font-size: 14px;
    color: var(--muted);
    letter-spacing: 0.3em;
    text-transform: uppercase;
    margin-bottom: 24px;
    opacity: 0;
    animation: fadeSlideUp 0.9s 0.35s ease forwards;
  }

  .hero-desc {
    max-width: 520px;
    margin: 0 auto 40px;
    font-size: 15px;
    line-height: 1.8;
    color: #8b949e;
    opacity: 0;
    animation: fadeSlideUp 0.9s 0.5s ease forwards;
  }

  .hero-links {
    display: flex;
    gap: 12px;
    justify-content: center;
    flex-wrap: wrap;
    opacity: 0;
    animation: fadeSlideUp 0.9s 0.65s ease forwards;
  }

  .btn {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    padding: 10px 20px;
    border-radius: 8px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 13px;
    text-decoration: none;
    transition: all 0.25s ease;
    position: relative;
    overflow: hidden;
  }
  .btn::before {
    content: '';
    position: absolute;
    inset: 0;
    opacity: 0;
    transition: opacity 0.25s;
  }
  .btn:hover::before { opacity: 1; }
  .btn-primary {
    background: var(--accent);
    color: var(--bg);
    font-weight: 700;
  }
  .btn-primary:hover { transform: translateY(-2px); box-shadow: 0 8px 24px rgba(0,212,255,0.3); }
  .btn-secondary {
    background: transparent;
    color: var(--text);
    border: 1px solid var(--border);
  }
  .btn-secondary:hover { border-color: var(--accent); color: var(--accent); transform: translateY(-2px); }

  /* Section styling */
  .section {
    margin-bottom: 64px;
    opacity: 0;
    transform: translateY(30px);
    transition: opacity 0.7s ease, transform 0.7s ease;
  }
  .section.visible { opacity: 1; transform: translateY(0); }

  .section-label {
    display: flex;
    align-items: center;
    gap: 12px;
    margin-bottom: 28px;
    font-size: 11px;
    letter-spacing: 0.25em;
    text-transform: uppercase;
    color: var(--accent);
  }
  .section-label::after {
    content: '';
    flex: 1;
    height: 1px;
    background: linear-gradient(90deg, var(--accent) 0%, transparent 100%);
    opacity: 0.3;
  }

  /* About cards */
  .about-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 16px;
  }
  .about-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 20px;
    transition: all 0.3s ease;
    position: relative;
    overflow: hidden;
  }
  .about-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: var(--accent);
    transform: scaleX(0);
    transition: transform 0.3s ease;
    transform-origin: left;
  }
  .about-card:hover::before { transform: scaleX(1); }
  .about-card:hover { border-color: rgba(0,212,255,0.3); transform: translateY(-4px); box-shadow: 0 12px 32px rgba(0,0,0,0.4); }
  .card-icon { font-size: 24px; margin-bottom: 12px; }
  .card-title { font-size: 12px; color: var(--muted); letter-spacing: 0.1em; text-transform: uppercase; margin-bottom: 6px; }
  .card-value { font-size: 14px; color: var(--text); font-weight: 700; }

  /* Tech stack */
  .tech-categories { display: flex; flex-direction: column; gap: 20px; }
  .tech-category {}
  .tech-cat-label {
    font-size: 11px;
    color: var(--muted);
    letter-spacing: 0.2em;
    text-transform: uppercase;
    margin-bottom: 10px;
  }
  .tech-tags { display: flex; flex-wrap: wrap; gap: 8px; }
  .tag {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    padding: 6px 14px;
    border-radius: 6px;
    font-size: 12px;
    font-weight: 700;
    border: 1px solid;
    transition: all 0.25s ease;
    cursor: default;
    letter-spacing: 0.05em;
  }
  .tag:hover { transform: translateY(-3px) scale(1.05); box-shadow: 0 6px 20px rgba(0,0,0,0.4); }

  .tag-php { background: rgba(119,107,180,0.15); border-color: rgba(119,107,180,0.4); color: #a78bfa; }
  .tag-laravel { background: rgba(255,45,32,0.12); border-color: rgba(255,45,32,0.35); color: #ff6b6b; }
  .tag-java { background: rgba(237,139,0,0.12); border-color: rgba(237,139,0,0.35); color: #fbbf24; }
  .tag-spring { background: rgba(109,179,63,0.12); border-color: rgba(109,179,63,0.35); color: #86efac; }
  .tag-js { background: rgba(247,223,30,0.1); border-color: rgba(247,223,30,0.3); color: #fde047; }
  .tag-react { background: rgba(97,218,251,0.1); border-color: rgba(97,218,251,0.3); color: #67e8f9; }
  .tag-mysql { background: rgba(68,121,161,0.15); border-color: rgba(68,121,161,0.4); color: #7dd3fc; }
  .tag-firebase { background: rgba(255,202,40,0.1); border-color: rgba(255,202,40,0.3); color: #fcd34d; }
  .tag-mongo { background: rgba(78,169,75,0.12); border-color: rgba(78,169,75,0.35); color: #4ade80; }
  .tag-default { background: rgba(0,212,255,0.08); border-color: rgba(0,212,255,0.25); color: var(--accent); }

  /* Project card */
  .project-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 32px;
    position: relative;
    overflow: hidden;
    transition: all 0.35s ease;
  }
  .project-card::after {
    content: '';
    position: absolute;
    inset: 0;
    background: radial-gradient(600px circle at var(--mouse-x, 50%) var(--mouse-y, 50%), rgba(0,212,255,0.04), transparent 40%);
    opacity: 0;
    transition: opacity 0.3s;
  }
  .project-card:hover::after { opacity: 1; }
  .project-card:hover { border-color: rgba(0,212,255,0.25); transform: translateY(-4px); box-shadow: 0 20px 60px rgba(0,0,0,0.5); }

  .project-header { display: flex; align-items: flex-start; justify-content: space-between; margin-bottom: 16px; flex-wrap: wrap; gap: 12px; }
  .project-name {
    font-family: 'Syne', sans-serif;
    font-size: 22px;
    font-weight: 800;
    color: var(--text);
  }
  .project-badge {
    background: rgba(127,255,110,0.12);
    border: 1px solid rgba(127,255,110,0.3);
    color: var(--accent3);
    padding: 4px 12px;
    border-radius: 100px;
    font-size: 11px;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    animation: badge-glow 3s ease infinite;
  }
  @keyframes badge-glow {
    0%, 100% { box-shadow: 0 0 0 0 rgba(127,255,110,0.2); }
    50% { box-shadow: 0 0 12px 2px rgba(127,255,110,0.15); }
  }
  .project-desc { color: var(--muted); font-size: 14px; line-height: 1.8; margin-bottom: 20px; }
  .project-features { display: flex; flex-direction: column; gap: 8px; }
  .feature {
    display: flex;
    align-items: center;
    gap: 10px;
    font-size: 13px;
    color: #8b949e;
    padding: 8px 12px;
    background: rgba(255,255,255,0.02);
    border-radius: 8px;
    border-left: 2px solid transparent;
    transition: all 0.2s;
  }
  .feature:hover { border-left-color: var(--accent); background: rgba(0,212,255,0.05); color: var(--text); }
  .feature-dot { color: var(--accent); font-size: 16px; }

  /* Learning section */
  .learning-items { display: flex; flex-direction: column; gap: 12px; }
  .learn-item {
    display: flex;
    align-items: center;
    gap: 16px;
    padding: 16px 20px;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 10px;
    transition: all 0.25s ease;
  }
  .learn-item:hover { border-color: rgba(0,212,255,0.3); transform: translateX(6px); }
  .learn-icon { font-size: 20px; }
  .learn-text { flex: 1; }
  .learn-title { font-size: 14px; font-weight: 700; margin-bottom: 2px; }
  .learn-sub { font-size: 12px; color: var(--muted); }
  .learn-progress {
    width: 80px;
    height: 4px;
    background: var(--border);
    border-radius: 100px;
    overflow: hidden;
  }
  .learn-bar {
    height: 100%;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    border-radius: 100px;
    animation: grow-bar 1.5s ease forwards;
    transform-origin: left;
    transform: scaleX(0);
  }
  @keyframes grow-bar { to { transform: scaleX(1); } }

  /* Stats */
  .stats-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 16px;
  }
  .stat-img {
    width: 100%;
    border-radius: 12px;
    border: 1px solid var(--border);
    transition: all 0.3s ease;
    display: block;
  }
  .stat-img:hover { border-color: rgba(0,212,255,0.3); transform: scale(1.02); }

  /* Footer */
  .footer {
    text-align: center;
    padding-top: 40px;
    border-top: 1px solid var(--border);
    color: var(--muted);
    font-size: 12px;
    letter-spacing: 0.1em;
  }
  .footer-quote {
    font-style: italic;
    color: rgba(0,212,255,0.5);
    margin-top: 8px;
    font-size: 13px;
  }

  /* Animations */
  @keyframes fadeSlideDown {
    from { opacity: 0; transform: translateY(-20px); }
    to { opacity: 1; transform: translateY(0); }
  }
  @keyframes fadeSlideUp {
    from { opacity: 0; transform: translateY(24px); }
    to { opacity: 1; transform: translateY(0); }
  }

  /* Scanline effect */
  .scanline {
    position: fixed;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, transparent, var(--accent), transparent);
    opacity: 0.3;
    animation: scan 4s linear infinite;
    pointer-events: none;
    z-index: 100;
  }
  @keyframes scan {
    0% { top: -2px; }
    100% { top: 100vh; }
  }

  /* Typing cursor */
  .typing::after {
    content: '|';
    animation: blink 1s step-end infinite;
    color: var(--accent);
  }
  @keyframes blink {
    0%, 100% { opacity: 1; }
    50% { opacity: 0; }
  }
</style>
</head>
<body>

<div class="cursor" id="cursor"></div>
<div class="cursor-trail" id="cursorTrail"></div>
<div class="scanline"></div>

<!-- Particles -->
<div class="particles" id="particles"></div>

<div class="container">

  <!-- HERO -->
  <section class="hero">
    <div class="status-bar">
      <div class="status-dot"></div>
      available for opportunities · malaysia
    </div>
    <h1 class="hero-name">
      <span>AKMAL</span>
      HAKIM
    </h1>
    <p class="hero-title">Backend Developer · Full-Stack Explorer</p>
    <p class="hero-desc">
      Building real-world web applications with clean, maintainable code.<br>
      Passionate about systems that scale and backends that hold.
    </p>
    <div class="hero-links">
      <a href="https://www.linkedin.com/in/akmal-hakim-bin-jamaluddin-a162a91b9/" class="btn btn-primary">💼 LinkedIn</a>
      <a href="https://github.com/akmalhakim05" class="btn btn-secondary">🐙 GitHub</a>
      <a href="https://bsky.app/profile/AKMAL%20HAKIM" class="btn btn-secondary">🦋 Bluesky</a>
    </div>
  </section>

  <!-- ABOUT -->
  <section class="section" id="s1">
    <div class="section-label">// about</div>
    <div class="about-grid">
      <div class="about-card">
        <div class="card-icon">📍</div>
        <div class="card-title">Location</div>
        <div class="card-value">Malaysia</div>
      </div>
      <div class="about-card">
        <div class="card-icon">🔧</div>
        <div class="card-title">Focus</div>
        <div class="card-value">Backend Systems</div>
      </div>
      <div class="about-card">
        <div class="card-icon">🚀</div>
        <div class="card-title">Approach</div>
        <div class="card-value">Clean & Scalable</div>
      </div>
      <div class="about-card">
        <div class="card-icon">🌱</div>
        <div class="card-title">Mode</div>
        <div class="card-value typing">Always Learning</div>
      </div>
    </div>
  </section>

  <!-- TECH STACK -->
  <section class="section" id="s2">
    <div class="section-label">// tech stack</div>
    <div class="tech-categories">
      <div class="tech-category">
        <div class="tech-cat-label">Languages</div>
        <div class="tech-tags">
          <span class="tag tag-php">PHP</span>
          <span class="tag tag-java">Java</span>
          <span class="tag tag-js">JavaScript</span>
          <span class="tag tag-default">HTML5</span>
        </div>
      </div>
      <div class="tech-category">
        <div class="tech-cat-label">Frameworks</div>
        <div class="tech-tags">
          <span class="tag tag-laravel">Laravel</span>
          <span class="tag tag-spring">Spring Boot</span>
          <span class="tag tag-react">React</span>
          <span class="tag tag-react">React Native</span>
          <span class="tag tag-default">Next.js</span>
          <span class="tag tag-laravel">Livewire</span>
        </div>
      </div>
      <div class="tech-category">
        <div class="tech-cat-label">Databases</div>
        <div class="tech-tags">
          <span class="tag tag-mysql">MySQL</span>
          <span class="tag tag-mongo">MongoDB</span>
          <span class="tag tag-default">SQLite</span>
          <span class="tag tag-firebase">Firebase</span>
        </div>
      </div>
      <div class="tech-category">
        <div class="tech-cat-label">DevOps & Tools</div>
        <div class="tech-tags">
          <span class="tag tag-default">Git</span>
          <span class="tag tag-default">Apache</span>
          <span class="tag tag-spring">Nginx</span>
          <span class="tag tag-default">Vercel</span>
          <span class="tag tag-default">Selenium</span>
        </div>
      </div>
    </div>
  </section>

  <!-- FEATURED PROJECT -->
  <section class="section" id="s3">
    <div class="section-label">// featured project</div>
    <div class="project-card" id="projectCard">
      <div class="project-header">
        <div class="project-name">🌟 Fundizen</div>
        <div class="project-badge">✦ Featured</div>
      </div>
      <p class="project-desc">
        A backend-focused charity crowdfunding platform — managing campaigns, donations, and users with secure authentication and robust data handling.
      </p>
      <div class="project-features">
        <div class="feature"><span class="feature-dot">▸</span> Secure user authentication &amp; role management</div>
        <div class="feature"><span class="feature-dot">▸</span> Campaign and donation tracking system</div>
        <div class="feature"><span class="feature-dot">▸</span> Structured MySQL database architecture</div>
        <div class="feature"><span class="feature-dot">▸</span> REST API design for clean frontend-backend separation</div>
      </div>
    </div>
  </section>

  <!-- LEARNING -->
  <section class="section" id="s4">
    <div class="section-label">// currently learning</div>
    <div class="learning-items">
      <div class="learn-item">
        <div class="learn-icon">☁️</div>
        <div class="learn-text">
          <div class="learn-title">Cloud Deployment</div>
          <div class="learn-sub">AWS · Docker · Container orchestration</div>
        </div>
        <div class="learn-progress"><div class="learn-bar" style="width:55%; animation-delay:0.2s"></div></div>
      </div>
      <div class="learn-item">
        <div class="learn-icon">⚙️</div>
        <div class="learn-text">
          <div class="learn-title">CI/CD Pipelines</div>
          <div class="learn-sub">Automation · Testing · Deployment workflows</div>
        </div>
        <div class="learn-progress"><div class="learn-bar" style="width:40%; animation-delay:0.4s"></div></div>
      </div>
      <div class="learn-item">
        <div class="learn-icon">🏗️</div>
        <div class="learn-text">
          <div class="learn-title">Backend Architecture</div>
          <div class="learn-sub">Scalable patterns · Best practices · System design</div>
        </div>
        <div class="learn-progress"><div class="learn-bar" style="width:65%; animation-delay:0.6s"></div></div>
      </div>
    </div>
  </section>

  <!-- STATS -->
  <section class="section" id="s5">
    <div class="section-label">// github stats</div>
    <div class="stats-grid">
      <img class="stat-img" src="https://github-readme-stats.vercel.app/api?username=akmalhakim05&theme=dark&hide_border=true&include_all_commits=true&count_private=false&bg_color=0d1117" alt="GitHub Stats">
      <img class="stat-img" src="https://nirzak-streak-stats.vercel.app/?user=akmalhakim05&theme=dark&hide_border=true&background=0d1117" alt="GitHub Streak">
    </div>
    <div style="margin-top:16px">
      <img class="stat-img" src="https://github-readme-stats.vercel.app/api/top-langs/?username=akmalhakim05&theme=dark&hide_border=true&include_all_commits=true&count_private=false&layout=compact&bg_color=0d1117" alt="Top Languages">
    </div>
  </section>

  <!-- FOOTER -->
  <footer class="footer section" id="s6">
    <p>AKMAL HAKIM · Backend Developer · Malaysia</p>
    <p class="footer-quote">"Clean code always looks like it was written by someone who cares."</p>
  </footer>

</div>

<script>
  // Custom cursor
  const cursor = document.getElementById('cursor');
  const trail = document.getElementById('cursorTrail');
  document.addEventListener('mousemove', e => {
    cursor.style.left = e.clientX + 'px';
    cursor.style.top = e.clientY + 'px';
    trail.style.left = e.clientX + 'px';
    trail.style.top = e.clientY + 'px';
  });

  // Project card glow on mouse move
  const card = document.getElementById('projectCard');
  card.addEventListener('mousemove', e => {
    const rect = card.getBoundingClientRect();
    const x = ((e.clientX - rect.left) / rect.width * 100) + '%';
    const y = ((e.clientY - rect.top) / rect.height * 100) + '%';
    card.style.setProperty('--mouse-x', x);
    card.style.setProperty('--mouse-y', y);
  });

  // Scroll reveal
  const sections = document.querySelectorAll('.section');
  const observer = new IntersectionObserver((entries) => {
    entries.forEach((e, i) => {
      if (e.isIntersecting) {
        setTimeout(() => e.target.classList.add('visible'), 100);
      }
    });
  }, { threshold: 0.1 });
  sections.forEach(s => observer.observe(s));

  // Particles
  const container = document.getElementById('particles');
  for (let i = 0; i < 30; i++) {
    const p = document.createElement('div');
    p.className = 'particle';
    p.style.left = Math.random() * 100 + 'vw';
    p.style.animationDuration = (8 + Math.random() * 12) + 's';
    p.style.animationDelay = (Math.random() * 10) + 's';
    p.style.width = p.style.height = (Math.random() > 0.7 ? '3px' : '2px');
    p.style.background = Math.random() > 0.5 ? 'var(--accent)' : 'var(--accent2)';
    container.appendChild(p);
  }
</script>
</body>
</html>
