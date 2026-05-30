<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Muhammad Rifanul Faiz — Video Editor & Motion Designer</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;0,9..40,500;1,9..40,300&family=DM+Serif+Display:ital@0;1&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --white: #ffffff;
    --off: #f7f6f3;
    --ink: #111110;
    --muted: #888880;
    --border: rgba(0,0,0,0.08);
    --accent: #111110;
    --radius: 4px;
  }

  html { scroll-behavior: smooth; }

  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--white);
    color: var(--ink);
    font-size: 15px;
    line-height: 1.6;
    -webkit-font-smoothing: antialiased;
    cursor: none;
  }

  /* Custom cursor */
  .cursor {
    width: 8px; height: 8px;
    background: var(--ink);
    border-radius: 50%;
    position: fixed;
    top: 0; left: 0;
    pointer-events: none;
    z-index: 9999;
    transition: transform 0.15s ease, width 0.2s ease, height 0.2s ease;
    transform: translate(-50%, -50%);
  }
  .cursor.expand { width: 40px; height: 40px; background: rgba(0,0,0,0.06); }

  /* Nav */
  nav {
    position: fixed; top: 0; left: 0; right: 0;
    z-index: 100;
    padding: 1.5rem 3rem;
    display: flex; justify-content: space-between; align-items: center;
    background: rgba(255,255,255,0.9);
    backdrop-filter: blur(12px);
    border-bottom: 1px solid var(--border);
    opacity: 0;
    animation: fadeDown 0.8s ease 0.2s forwards;
  }

  .nav-logo {
    font-family: 'DM Serif Display', serif;
    font-size: 1.1rem;
    color: var(--ink);
    text-decoration: none;
    letter-spacing: 0.01em;
  }

  .nav-links {
    display: flex; gap: 2rem; list-style: none;
  }

  .nav-links a {
    font-size: 13px;
    color: var(--muted);
    text-decoration: none;
    letter-spacing: 0.05em;
    text-transform: uppercase;
    transition: color 0.2s;
  }
  .nav-links a:hover { color: var(--ink); }

  /* Hero */
  .hero {
    min-height: 100vh;
    display: flex; flex-direction: column; justify-content: flex-end;
    padding: 0 3rem 4rem;
    position: relative;
    overflow: hidden;
  }

  .hero-bg {
    position: absolute; inset: 0;
    background: var(--off);
    z-index: 0;
  }

  .hero-grain {
    position: absolute; inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
    background-size: 200px;
    z-index: 1;
    opacity: 0.5;
  }

  .hero-content { position: relative; z-index: 2; }

  .hero-tag {
    display: inline-block;
    font-size: 11px;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--muted);
    border: 1px solid var(--border);
    padding: 6px 14px;
    border-radius: 100px;
    margin-bottom: 2rem;
    opacity: 0;
    animation: fadeUp 0.8s ease 0.5s forwards;
  }

  .hero-title {
    font-family: 'DM Serif Display', serif;
    font-size: clamp(3rem, 8vw, 7rem);
    line-height: 1.0;
    letter-spacing: -0.02em;
    margin-bottom: 2rem;
    opacity: 0;
    animation: fadeUp 0.9s ease 0.6s forwards;
  }

  .hero-title em {
    font-style: italic;
    color: var(--muted);
  }

  .hero-bottom {
    display: flex;
    justify-content: space-between;
    align-items: flex-end;
    opacity: 0;
    animation: fadeUp 0.9s ease 0.8s forwards;
  }

  .hero-desc {
    max-width: 380px;
    font-size: 15px;
    color: var(--muted);
    font-weight: 300;
    line-height: 1.7;
  }

  .hero-stats {
    display: flex; gap: 3rem; text-align: right;
  }

  .stat-num {
    display: block;
    font-family: 'DM Serif Display', serif;
    font-size: 2rem;
    line-height: 1;
    margin-bottom: 4px;
  }

  .stat-label {
    font-size: 11px;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    color: var(--muted);
  }

  /* Scroll indicator */
  .scroll-indicator {
    position: absolute;
    bottom: 2rem; left: 50%;
    transform: translateX(-50%);
    display: flex; flex-direction: column; align-items: center; gap: 8px;
    opacity: 0;
    animation: fadeUp 1s ease 1.2s forwards;
    z-index: 2;
  }

  .scroll-indicator span {
    font-size: 10px;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--muted);
  }

  .scroll-line {
    width: 1px; height: 40px;
    background: linear-gradient(to bottom, var(--muted), transparent);
    animation: scrollPulse 2s ease-in-out infinite;
  }

  /* Section base */
  section { padding: 6rem 3rem; }

  .section-label {
    font-size: 11px;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--muted);
    margin-bottom: 3rem;
    display: flex; align-items: center; gap: 1rem;
  }

  .section-label::after {
    content: '';
    flex: 1;
    height: 1px;
    background: var(--border);
  }

  /* Work section */
  #work { background: var(--white); }

  .work-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 2px;
  }

  .work-item {
    position: relative;
    overflow: hidden;
    background: var(--off);
    aspect-ratio: 16/10;
    cursor: none;
  }

  .work-item.full { grid-column: 1 / -1; aspect-ratio: 16/7; }

  .work-thumb {
    width: 100%; height: 100%;
    position: relative;
    overflow: hidden;
  }

  .work-thumb iframe {
    width: 100%; height: 100%;
    border: none;
    pointer-events: none;
    transform: scale(1.02);
    transition: transform 0.6s ease;
  }

  .work-item:hover .work-thumb iframe { transform: scale(1.06); }

  .work-overlay {
    position: absolute; inset: 0;
    background: rgba(0,0,0,0);
    transition: background 0.3s ease;
    display: flex; flex-direction: column; justify-content: flex-end;
    padding: 1.5rem;
  }

  .work-item:hover .work-overlay { background: rgba(0,0,0,0.45); }

  .work-info {
    transform: translateY(12px);
    opacity: 0;
    transition: all 0.3s ease;
  }

  .work-item:hover .work-info { transform: translateY(0); opacity: 1; }

  .work-title {
    font-family: 'DM Serif Display', serif;
    font-size: 1.3rem;
    color: white;
    margin-bottom: 4px;
  }

  .work-meta {
    font-size: 12px;
    letter-spacing: 0.06em;
    text-transform: uppercase;
    color: rgba(255,255,255,0.6);
  }

  .play-btn {
    position: absolute;
    top: 50%; left: 50%;
    transform: translate(-50%, -50%) scale(0.8);
    width: 56px; height: 56px;
    background: white;
    border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    opacity: 0;
    transition: all 0.3s ease;
    text-decoration: none;
  }

  .play-btn svg { margin-left: 3px; }

  .work-item:hover .play-btn {
    opacity: 1;
    transform: translate(-50%, -50%) scale(1);
  }

  /* About */
  #about {
    background: var(--off);
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 6rem;
    align-items: start;
  }

  .about-left { }

  .about-title {
    font-family: 'DM Serif Display', serif;
    font-size: clamp(2rem, 4vw, 3.5rem);
    line-height: 1.1;
    margin-bottom: 2rem;
    letter-spacing: -0.01em;
  }

  .about-title em { font-style: italic; color: var(--muted); }

  .about-text {
    color: var(--muted);
    font-weight: 300;
    line-height: 1.8;
    margin-bottom: 2.5rem;
    font-size: 15px;
  }

  .tools-list {
    display: flex; flex-wrap: wrap; gap: 8px;
  }

  .tool-tag {
    font-size: 12px;
    letter-spacing: 0.04em;
    padding: 6px 14px;
    border: 1px solid var(--border);
    border-radius: 100px;
    color: var(--muted);
    background: white;
  }

  .about-right { padding-top: 1rem; }

  .service-item {
    padding: 1.5rem 0;
    border-bottom: 1px solid var(--border);
  }

  .service-item:first-child { border-top: 1px solid var(--border); }

  .service-num {
    font-size: 11px;
    color: var(--muted);
    letter-spacing: 0.08em;
    margin-bottom: 8px;
  }

  .service-name {
    font-size: 1rem;
    font-weight: 500;
    margin-bottom: 6px;
  }

  .service-desc {
    font-size: 13px;
    color: var(--muted);
    font-weight: 300;
  }

  /* CTA */
  #contact {
    background: var(--ink);
    color: white;
    text-align: center;
    padding: 8rem 3rem;
  }

  .cta-label {
    font-size: 11px;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: rgba(255,255,255,0.4);
    margin-bottom: 2rem;
  }

  .cta-title {
    font-family: 'DM Serif Display', serif;
    font-size: clamp(2.5rem, 6vw, 5rem);
    line-height: 1.05;
    letter-spacing: -0.02em;
    margin-bottom: 2.5rem;
  }

  .cta-title em { font-style: italic; color: rgba(255,255,255,0.4); }

  .cta-btn {
    display: inline-block;
    padding: 1rem 2.5rem;
    border: 1px solid rgba(255,255,255,0.2);
    color: white;
    text-decoration: none;
    font-size: 13px;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    border-radius: 100px;
    transition: all 0.3s ease;
    margin: 0.5rem;
  }

  .cta-btn:hover {
    background: white;
    color: var(--ink);
    border-color: white;
  }

  .cta-btn.primary {
    background: white;
    color: var(--ink);
    border-color: white;
  }

  .cta-btn.primary:hover {
    background: transparent;
    color: white;
  }

  /* Footer */
  footer {
    background: var(--ink);
    border-top: 1px solid rgba(255,255,255,0.06);
    padding: 2rem 3rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
    color: rgba(255,255,255,0.3);
    font-size: 12px;
  }

  .footer-logo {
    font-family: 'DM Serif Display', serif;
    color: rgba(255,255,255,0.5);
    font-size: 1rem;
  }

  /* Animations */
  @keyframes fadeDown {
    from { opacity: 0; transform: translateY(-10px); }
    to { opacity: 1; transform: translateY(0); }
  }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(20px); }
    to { opacity: 1; transform: translateY(0); }
  }

  @keyframes scrollPulse {
    0%, 100% { opacity: 0.3; transform: scaleY(1); }
    50% { opacity: 1; transform: scaleY(1.1); }
  }

  /* Scroll reveal */
  .reveal {
    opacity: 0;
    transform: translateY(30px);
    transition: opacity 0.8s ease, transform 0.8s ease;
  }
  .reveal.visible { opacity: 1; transform: translateY(0); }

  @media (max-width: 768px) {
    nav { padding: 1.2rem 1.5rem; }
    .hero { padding: 0 1.5rem 3rem; }
    .hero-stats { display: none; }
    .work-grid { grid-template-columns: 1fr; }
    .work-item.full { grid-column: 1; }
    #about { grid-template-columns: 1fr; gap: 3rem; padding: 4rem 1.5rem; }
    section { padding: 4rem 1.5rem; }
    #contact { padding: 5rem 1.5rem; }
    footer { flex-direction: column; gap: 1rem; text-align: center; }
    body { cursor: auto; }
    .cursor { display: none; }
  }
</style>
</head>
<body>

<div class="cursor" id="cursor"></div>

<nav>
  <a href="#" class="nav-logo">Faiz</a>
  <ul class="nav-links">
    <li><a href="#work">Work</a></li>
    <li><a href="#about">About</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
</nav>

<!-- Hero -->
<section class="hero" id="home">
  <div class="hero-bg"></div>
  <div class="hero-grain"></div>
  <div class="hero-content">
    <div class="hero-tag">Video Editor & Motion Graphics Designer</div>
    <h1 class="hero-title">
      Frames that<br><em>move</em> people.
    </h1>
    <div class="hero-bottom">
      <p class="hero-desc">
        Short-form, long-form, and kinetic typography — crafted to maximize audience retention metrics and conversion.
      </p>
      <div class="hero-stats">
        <div>
          <span class="stat-num">4+</span>
          <span class="stat-label">Years editing</span>
        </div>
      </div>
    </div>
  </div>
  <div class="scroll-indicator">
    <div class="scroll-line"></div>
    <span>Scroll</span>
  </div>
</section>

<!-- Work -->
<section id="work">
  <div class="section-label reveal">Selected Work</div>
  <div class="work-grid">

    <!-- Long-form -->
    <div class="work-item full reveal">
      <div class="work-thumb">
        <iframe
          src="https://drive.google.com/file/d/15Qc9Btc7FFqa57fHd6a74k8fUuPObzHh/preview"
          allow="autoplay"
          allowfullscreen>
        </iframe>
      </div>
      <div class="work-overlay">
        <a class="play-btn" href="https://drive.google.com/file/d/15Qc9Btc7FFqa57fHd6a74k8fUuPObzHh/view" target="_blank">
          <svg width="14" height="16" viewBox="0 0 14 16" fill="none">
            <path d="M1 1l12 7-12 7V1z" fill="#111"/>
          </svg>
        </a>
        <div class="work-info">
          <div class="work-title">Long-Form — Ben Ewert</div>
          <div class="work-meta">YouTube · Storytelling · Retention-focused</div>
        </div>
      </div>
    </div>

    <!-- Motion Graphics -->
    <div class="work-item reveal">
      <div class="work-thumb">
        <iframe
          src="https://drive.google.com/file/d/1p5lNWFtpay8tvRL2oEhlrZB1QR2gSB2e/preview"
          allow="autoplay"
          allowfullscreen>
        </iframe>
      </div>
      <div class="work-overlay">
        <a class="play-btn" href="https://drive.google.com/file/d/1p5lNWFtpay8tvRL2oEhlrZB1QR2gSB2e/view" target="_blank">
          <svg width="14" height="16" viewBox="0 0 14 16" fill="none">
            <path d="M1 1l12 7-12 7V1z" fill="#111"/>
          </svg>
        </a>
        <div class="work-info">
          <div class="work-title">Simple Motion Graphics</div>
          <div class="work-meta">After Effects · Motion Design · Expressions</div>
        </div>
      </div>
    </div>

    <!-- Explainer -->
    <div class="work-item reveal">
      <div class="work-thumb">
        <iframe
          src="https://drive.google.com/file/d/17bSlZd8su72vA_40M385Vsp15Iwj_kEh/preview"
          allow="autoplay"
          allowfullscreen>
        </iframe>
      </div>
      <div class="work-overlay">
        <a class="play-btn" href="https://drive.google.com/file/d/17bSlZd8su72vA_40M385Vsp15Iwj_kEh/view" target="_blank">
          <svg width="14" height="16" viewBox="0 0 14 16" fill="none">
            <path d="M1 1l12 7-12 7V1z" fill="#111"/>
          </svg>
        </a>
        <div class="work-info">
          <div class="work-title">Explainer Video</div>
          <div class="work-meta">Educational · Script-to-screen</div>
        </div>
      </div>
    </div>

    <!-- Short-form -->
    <div class="work-item reveal" style="grid-column: 1 / -1; aspect-ratio: 16/7;">
      <div class="work-thumb">
        <iframe
          src="https://drive.google.com/file/d/159MqEUHm1uCBOGPkswrzyIDYH9IxcMM7/preview"
          allow="autoplay"
          allowfullscreen>
        </iframe>
      </div>
      <div class="work-overlay">
        <a class="play-btn" href="https://drive.google.com/file/d/159MqEUHm1uCBOGPkswrzyIDYH9IxcMM7/view" target="_blank">
          <svg width="14" height="16" viewBox="0 0 14 16" fill="none">
            <path d="M1 1l12 7-12 7V1z" fill="#111"/>
          </svg>
        </a>
        <div class="work-info">
          <div class="work-title">Short-Form</div>
          <div class="work-meta">TikTok · Reels · Shorts · Hook-first pacing</div>
        </div>
      </div>
    </div>

  </div>
</section>

<!-- About -->
<section id="about">
  <div class="about-left reveal">
    <div class="section-label">About</div>
    <h2 class="about-title">
      Editing with<br><em>intent</em>, not<br>just instinct.
    </h2>
    <p class="about-text">
      I'm Muhammad Rifanul Faiz — an 18-year-old freelance video editor and motion graphics designer based in Pontianak, Indonesia. I craft content for international creators and agencies, specializing in short-form that hooks, long-form that retains, and motion graphics that actually say something.
    </p>
    <p class="about-text">
      My workflow is built around precision and engagement. I integrate precise audio transcriptions (US, UK, and Australian conventions) and utilize advanced After Effects techniques for complex kinetic typography.
    </p>
    <div class="tools-list">
      <span class="tool-tag">Premiere Pro</span>
      <span class="tool-tag">After Effects</span>
      <span class="tool-tag">CapCut</span>
      <span class="tool-tag">Attention Audits</span>
      <span class="tool-tag">AI-Generated Assets</span>
    </div>
  </div>
  <div class="about-right reveal">
    <div class="section-label">Services</div>
    <div class="service-item">
      <div class="service-num">01</div>
      <div class="service-name">Short-Form Editing</div>
      <div class="service-desc">TikTok, Reels, Shorts — fast pacing, strong hooks, optimized for maximum retention metrics.</div>
    </div>
    <div class="service-item">
      <div class="service-num">02</div>
      <div class="service-name">Long-Form YouTube</div>
      <div class="service-desc">Story-driven edits structured for watch time, utilizing precise pacing and attention audits.</div>
    </div>
    <div class="service-item">
      <div class="service-num">03</div>
      <div class="service-name">Motion Graphics</div>
      <div class="service-desc">Advanced UI-style animations, kinetic typography with precise formatting, and custom branded motion in After Effects.</div>
    </div>
    <div class="service-item">
      <div class="service-num">04</div>
      <div class="service-name">AI-Integrated Workflow</div>
      <div class="service-desc">Faster turnaround with AI-generated visual assets, smart automation, and precise audio transcription tools.</div>
    </div>
  </div>
</section>

<!-- CTA -->
<section id="contact">
  <div class="cta-label">Ready to work?</div>
  <h2 class="cta-title">
    Let's make<br>something <em>worth</em><br>watching.
  </h2>
  <div>
    <a href="mailto:email-lo-disini@gmail.com" target="_blank" class="cta-btn primary">Get in touch</a>
  </div>
</section>

<footer>
  <span class="footer-logo">Rifanul</span>
  <span>© 2026 Muhammad Rifanul Faiz. All rights reserved.</span>
  <span>Pontianak, Indonesia</span>
</footer>

<script>
  // Custom cursor
  const cursor = document.getElementById('cursor');
  document.addEventListener('mousemove', e => {
    cursor.style.left = e.clientX + 'px';
    cursor.style.top = e.clientY + 'px';
  });
  document.querySelectorAll('a, .work-item, button').forEach(el => {
    el.addEventListener('mouseenter', () => cursor.classList.add('expand'));
    el.addEventListener('mouseleave', () => cursor.classList.remove('expand'));
  });

  // Scroll reveal
  const reveals = document.querySelectorAll('.reveal');
  const observer = new IntersectionObserver(entries => {
    entries.forEach((entry, i) => {
      if (entry.isIntersecting) {
        setTimeout(() => entry.target.classList.add('visible'), i * 80);
        observer.unobserve(entry.target);
      }
    });
  }, { threshold: 0.1 });
  reveals.forEach(el => observer.observe(el));
</script>
</body>
</html>
