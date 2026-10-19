<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>JOHN DOE | Chaos Developer</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;700&family=Syne:wght@800&display=swap" rel="stylesheet">
<style>
:root{
  --bg:#060a1a; --panel:#0b1230; --ink:#e8f1ff; --dim:#8da2c8;
  --c1:#00e5ff; --c2:#ff2bd6; --c3:#ffb800; --sv:0;
  --display:'Syne','Arial Black',system-ui,sans-serif;
  --body:'Space Grotesk','Hiragino Sans','Noto Sans JP',system-ui,sans-serif;
}
*{box-sizing:border-box;margin:0;padding:0}
html{scroll-behavior:smooth}
body{background:var(--bg);color:var(--ink);font-family:var(--body);line-height:1.7;overflow-x:hidden}
a{color:inherit;text-decoration:none}
:focus-visible{outline:2px solid var(--c1);outline-offset:3px}
canvas{position:fixed;inset:0;width:100%;height:100%;pointer-events:none}
#bg{z-index:0}
#fx{z-index:30}
body::after{content:"";position:fixed;inset:0;z-index:29;pointer-events:none;opacity:.35;
  background:repeating-linear-gradient(0deg,rgba(0,0,0,.18) 0 1px,transparent 1px 3px);transition:opacity .4s}
body.chaos::after{opacity:1;animation:flick .12s infinite steps(2)}
@keyframes flick{50%{transform:translateY(1px)}}

header{position:fixed;top:0;left:0;right:0;z-index:10;display:flex;justify-content:space-between;align-items:center;
  padding:14px clamp(16px,4vw,48px);background:linear-gradient(var(--bg),transparent);backdrop-filter:blur(6px)}
.logo{font-family:var(--display);font-size:1.5rem;letter-spacing:.04em;cursor:pointer;user-select:none;
  text-shadow:0 0 12px var(--c1)}
nav{display:flex;gap:clamp(12px,3vw,32px);font-size:.9rem;color:var(--dim)}
nav a:hover{color:var(--c1);text-shadow:0 0 10px var(--c1)}

main{position:relative;z-index:1}
section{max-width:1100px;margin:0 auto;padding:110px clamp(18px,5vw,48px) 20px}
.hero{min-height:100svh;display:flex;flex-direction:column;justify-content:center;padding-top:90px}
h1,h2{font-family:var(--display);line-height:.92;
  text-shadow:calc(var(--sv)*9px) 0 var(--c2),calc(var(--sv)*-9px) 0 var(--c1)}
h1{font-size:clamp(3.4rem,15vw,11rem);text-shadow:calc(var(--sv)*9px) 0 var(--c2),calc(var(--sv)*-9px) 0 var(--c1),0 0 40px rgba(0,229,255,.3)}
h2{font-size:clamp(2rem,6vw,3.4rem);margin-bottom:28px;display:flex;align-items:center;gap:16px}
h2::after{content:"";height:2px;flex:1;background:linear-gradient(90deg,var(--c1),var(--c2),transparent);box-shadow:0 0 12px var(--c1)}
.tagline{font-size:clamp(1.05rem,2.6vw,1.6rem);margin-top:22px;max-width:30ch;color:var(--ink)}
.lede{color:var(--dim);margin-top:8px}
.cta{display:inline-block;margin-top:34px;padding:12px 28px;border:1px solid var(--c1);color:var(--c1);border-radius:999px;
  width:fit-content;transition:.25s;box-shadow:0 0 18px rgba(0,229,255,.25)}
.cta:hover{background:var(--c1);color:var(--bg);box-shadow:0 0 34px var(--c1)}
#readout{margin-top:40px;font-size:.78rem;color:var(--dim);font-family:ui-monospace,Menlo,Consolas,monospace}

/* glitch */
.glitch{position:relative}
.glitch::before,.glitch::after{content:attr(data-text);position:absolute;inset:0;opacity:0;pointer-events:none}
.glitch::before{color:var(--c1);text-shadow:none}
.glitch::after{color:var(--c2);text-shadow:none}
.chaos .glitch::before{opacity:.9;animation:gl1 .7s infinite steps(1)}
.chaos .glitch::after{opacity:.9;animation:gl2 .9s infinite steps(1)}
@keyframes gl1{0%{clip-path:inset(10% 0 80% 0);transform:translate(-7px)}20%{clip-path:inset(60% 0 10% 0);transform:translate(6px)}
  40%{clip-path:inset(30% 0 50% 0);transform:translate(-4px)}60%{clip-path:inset(80% 0 5% 0);transform:translate(5px)}
  80%{clip-path:inset(5% 0 70% 0);transform:translate(-8px)}100%{clip-path:inset(45% 0 35% 0);transform:translate(3px)}}
@keyframes gl2{0%{clip-path:inset(70% 0 10% 0);transform:translate(7px)}25%{clip-path:inset(15% 0 65% 0);transform:translate(-6px)}
  50%{clip-path:inset(50% 0 30% 0);transform:translate(5px)}75%{clip-path:inset(0 0 90% 0);transform:translate(-3px)}100%{clip-path:inset(85% 0 2% 0);transform:translate(8px)}}

/* about */
.about{display:grid;grid-template-columns:1.4fr 1fr;gap:clamp(20px,4vw,48px)}
.about p{color:#c4d3ef;max-width:60ch;margin-bottom:14px}
dl{display:grid;grid-template-columns:auto 1fr;gap:10px 18px;align-self:start;padding:22px;border:1px solid rgba(0,229,255,.25);
  background:rgba(11,18,48,.6);backdrop-filter:blur(6px);border-radius:14px}
dt{color:var(--c3)} dd{color:var(--ink)}

/* tags */
.tags{display:flex;flex-wrap:wrap;gap:12px}
.tag{padding:8px 18px;border-radius:999px;border:1px solid var(--tc,var(--c1));color:var(--tc,var(--c1));
  background:rgba(6,10,26,.6);transition:.2s;cursor:default}
.tag:nth-child(3n+2){--tc:var(--c2)} .tag:nth-child(3n){--tc:var(--c3)}
.tag:hover{background:var(--tc);color:var(--bg);box-shadow:0 0 22px var(--tc);transform:translateY(-3px) scale(1.06)}

/* cards */
.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(240px,1fr));gap:22px}
.card{--rx:0deg;--ry:0deg;--mx:50%;--my:50%;position:relative;padding:26px;border-radius:16px;overflow:hidden;
  background:linear-gradient(160deg,rgba(14,24,64,.85),rgba(8,12,34,.9));border:1px solid rgba(0,229,255,.22);
  transform:perspective(800px) rotateX(var(--rx)) rotateY(var(--ry));transition:transform .12s,box-shadow .25s,border-color .25s;will-change:transform}
.card::before{content:"";position:absolute;inset:0;pointer-events:none;opacity:0;transition:opacity .25s;
  background:radial-gradient(260px circle at var(--mx) var(--my),rgba(0,229,255,.22),rgba(255,43,214,.10) 45%,transparent 70%)}
.card:hover{border-color:var(--c1);box-shadow:0 0 0 1px var(--c1),0 0 34px rgba(0,229,255,.4),inset 0 0 34px rgba(255,43,214,.10)}
.card:hover::before{opacity:1}
.card h3{font-size:1.25rem;margin-bottom:8px;position:relative}
.card p{color:#b4c4e4;font-size:.95rem;position:relative}
.card .meta{margin-top:16px;color:var(--c3);font-size:.85rem;position:relative}

/* contact */
.contact p{color:#c4d3ef;margin-bottom:22px}
.links{display:flex;flex-wrap:wrap;gap:14px}
.links a{padding:12px 24px;border:1px solid var(--c2);color:var(--c2);border-radius:10px;transition:.25s}
.links a:hover{background:var(--c2);color:var(--bg);box-shadow:0 0 30px var(--c2);transform:translateY(-3px)}
footer{position:relative;z-index:1;text-align:center;padding:70px 16px 90px;color:var(--dim);font-size:.85rem}

/* chaos toggle */
#chaosBtn{position:fixed;right:clamp(14px,3vw,32px);bottom:clamp(14px,3vw,32px);z-index:40;padding:14px 22px;cursor:pointer;
  font:700 .95rem var(--body);color:var(--ink);background:rgba(6,10,26,.85);border:2px solid var(--c2);border-radius:999px;
  box-shadow:0 0 22px rgba(255,43,214,.5);backdrop-filter:blur(6px);transition:.2s}
#chaosBtn:hover{transform:scale(1.07)}
#chaosBtn[aria-pressed="true"]{border-color:var(--c3);color:var(--c3);box-shadow:0 0 36px var(--c3);animation:btnpulse .5s infinite alternate}
@keyframes btnpulse{to{transform:scale(1.08) rotate(-2deg)}}
#toast{position:fixed;left:50%;top:84px;z-index:50;transform:translate(-50%,-20px);opacity:0;padding:10px 22px;border-radius:999px;
  background:var(--c3);color:var(--bg);font-weight:700;transition:.3s;pointer-events:none;text-align:center}
#toast.show{opacity:1;transform:translate(-50%,0)}
main.shake{animation:shake .5s}
@keyframes shake{20%{transform:translate(-10px,6px)}40%{transform:translate(9px,-7px)}60%{transform:translate(-6px,-4px)}80%{transform:translate(5px,5px)}}

/* chaos mode */
.chaos h2{animation:rgb .3s infinite steps(2)}
@keyframes rgb{0%{text-shadow:6px 0 var(--c2),-6px 0 var(--c1)}100%{text-shadow:-5px 2px var(--c2),5px -2px var(--c1)}}
.chaos .card{animation:spin3d 5s infinite ease-in-out}
.chaos .card:nth-child(even){animation-direction:reverse;animation-duration:7s}
@keyframes spin3d{0%,100%{transform:perspective(800px) rotateY(0) rotateX(0)}
  25%{transform:perspective(800px) rotateY(28deg) rotateX(-12deg)}
  50%{transform:perspective(800px) rotateY(-24deg) rotateX(14deg) rotateZ(3deg)}
  75%{transform:perspective(800px) rotateY(16deg) rotateX(10deg) rotateZ(-3deg)}}
.chaos .tag{animation:wob .6s infinite alternate ease-in-out}
.chaos .tag:nth-child(odd){animation-delay:-.3s;animation-duration:.45s}
@keyframes wob{from{transform:rotate(-5deg) translateY(-3px)}to{transform:rotate(6deg) translateY(4px) scale(1.08)}}
.chaos .tagline,.chaos dl{animation:wob 1.2s infinite alternate ease-in-out}
.chaos .logo{animation:spin 1s infinite linear;display:inline-block}
@keyframes spin{to{transform:rotateY(360deg)}}

@media(max-width:760px){.about{grid-template-columns:1fr} section{padding-top:90px}}
@media(prefers-reduced-motion:reduce){
  .chaos *,.chaos *::before,.chaos *::after,main.shake{animation:none!important}
}
</style>
</head>
<body>
<canvas id="bg" aria-hidden="true"></canvas>
<canvas id="fx" aria-hidden="true"></canvas>

<header>
  <a class="logo" id="logo" aria-label="JOHN DOE">J/D</a>
  <nav>
    <a href="#about">About</a><a href="#skills">Skills</a><a href="#works">Works</a><a href="#contact">Contact</a>
  </nav>
</header>

<main id="main">
  <section class="hero" id="top">
    <h1 class="glitch" data-text="JOHN DOE">JOHN DOE</h1>
    <p class="tagline">Order is just chaos that hasn’t happened yet.</p>
    <p class="lede">Chaos Developer ／ わずかな違いが、まったく別の未来を描く。</p>
    <a class="cta" href="#works">View works</a>
    <div id="readout"></div>
  </section>

  <section id="about">
    <h2 class="glitch" data-text="About">About</h2>
    <div class="about">
      <div>
        <p>東京を拠点に、数式とノイズから生まれる動きをWebに落とし込んでいます。初期値がほんの少し違うだけで、まったく別の軌道を描く。そんなカオス理論の気まぐれさを、「触って楽しい」体験に変えるのが仕事です。</p>
        <p>仕事のご相談、共同制作、ただの雑談まで、お気軽にご連絡ください。</p>
      </div>
      <dl>
        <dt>Base</dt><dd>Tokyo, JP</dd>
        <dt>Role</dt><dd>Chaos Developer</dd>
        <dt>Focus</dt><dd>Generative art / Creative coding</dd>
        <dt>Status</dt><dd>Open to collaboration</dd>
      </dl>
    </div>
  </section>

  <section id="skills">
    <h2 class="glitch" data-text="Skills">Skills</h2>
    <div class="tags">
      <span class="tag">JavaScript</span><span class="tag">TypeScript</span><span class="tag">Canvas API</span>
      <span class="tag">WebGL</span><span class="tag">GLSL</span><span class="tag">Three.js</span>
      <span class="tag">React</span><span class="tag">Node.js</span><span class="tag">Python</span>
      <span class="tag">Rust / WASM</span><span class="tag">Numerical Simulation</span><span class="tag">Generative Art</span>
      <span class="tag">Creative Coding</span><span class="tag">Figma</span>
    </div>
  </section>

  <section id="works">
    <h2 class="glitch" data-text="Works">Works</h2>
    <div class="grid">
      <article class="card" data-tilt><h3>Lorenz Garden</h3><p>ローレンツ方程式から育つ、リアルタイムのジェネラティブアート。</p><div class="meta">Canvas / JavaScript</div></article>
      <article class="card" data-tilt><h3>Double Pendulum Lab</h3><p>二重振り子を並べて、初期条件の差が広がる様子を観察できる実験場。</p><div class="meta">Canvas / Physics</div></article>
      <article class="card" data-tilt><h3>Glitch Typesetter</h3><p>文字を壊して組み直す、タイポグラフィのためのツール。</p><div class="meta">CSS / JavaScript</div></article>
      <article class="card" data-tilt><h3>Noise Radio</h3><p>環境音をパーティクルに変換する、ブラウザの中の楽器。</p><div class="meta">Web Audio / WebGL</div></article>
    </div>
  </section>

  <section id="contact" class="contact">
    <h2 class="glitch" data-text="Contact">Contact</h2>
    <p>お仕事の依頼や制作の相談は、メールまたはSNSからどうぞ。</p>
    <div class="links">
      <a href="mailto:hello@example.com">hello@example.com</a>
      <a href="https://github.com/" target="_blank" rel="noopener">GitHub</a>
      <a href="https://x.com/" target="_blank" rel="noopener">X</a>
      <a href="https://www.linkedin.com/" target="_blank" rel="noopener">LinkedIn</a>
    </div>
  </section>
</main>

<footer>© 2026 JOHN DOE. Everything here is a little unpredictable.</footer>

<button id="chaosBtn" aria-pressed="false">Chaos mode: OFF</button>
<div id="toast" role="status"></div>

<script>
(() => {
  const $ = s => document.querySelector(s);
  const bg = $('#bg'), fx = $('#fx'), c = bg.getContext('2d'), f = fx.getContext('2d');
  const reduce = matchMedia('(prefers-reduced-motion: reduce)').matches;
  const base = reduce ? 0.4 : 1;
  let W, H, DPR, ps = [];
  let chaos = false, speed = base, t = 0, last = performance.now();
  let mx = -999, my = -999, nx = 0, sv = 0, lastY = scrollY, rho = 28;

  /* ---------- Lorenz attractors ---------- */
  const N = 8, tr = [];
  const lor = (p, dt, r) => {
    const dx = 10 * (p.y - p.x), dy = p.x * (r - p.z) - p.y, dz = p.x * p.y - (8 / 3) * p.z;
    p.x += dx * dt; p.y += dy * dt; p.z += dz * dt;
    if (!isFinite(p.x) || Math.abs(p.x) > 100) { p.x = 1; p.y = 1; p.z = 20; }
  };
  for (let i = 0; i < N; i++) {          // tiny differences in the starting point -> diverging paths
    const p = { x: 1 + i * 0.02, y: 1, z: 20, px: null, py: null };
    for (let k = 0; k < 400; k++) lor(p, 0.006, 28);
    tr.push(p);
  }

  function resize() {
    DPR = Math.min(devicePixelRatio || 1, 2); W = innerWidth; H = innerHeight;
    for (const k of [bg, fx]) { k.width = W * DPR; k.height = H * DPR; }
    c.setTransform(DPR, 0, 0, DPR, 0, 0); f.setTransform(DPR, 0, 0, DPR, 0, 0);
    c.fillStyle = '#060a1a'; c.fillRect(0, 0, W, H);
    const m = Math.max(50, Math.min(140, Math.round(W * H / 16000)));
    ps = Array.from({ length: m }, (_, k) => ({ x: Math.random() * W, y: Math.random() * H, v: .4 + Math.random() * .9, h: 180 + Math.random() * 140, k }));
    tr.forEach(p => { p.px = null; });
  }
  addEventListener('resize', resize); resize();

  /* ---------- FX particles (mouse trail + explosions) ---------- */
  const parts = [], hues = [185, 310, 45];
  function burst(x, y, n, pow = 1) {
    for (let i = 0; i < n; i++) {
      const a = Math.random() * 6.283, v = Math.sqrt(Math.random()) * 14 * pow;
      parts.push({ x, y, vx: Math.cos(a) * v, vy: Math.sin(a) * v, l: 1, d: .006 + Math.random() * .012,
        h: hues[(Math.random() * 3) | 0] + Math.random() * 25, r: 1 + Math.random() * 2.5 });
    }
    if (parts.length > 2500) parts.splice(0, parts.length - 2500);
  }
  function trail(x, y, n, v) {
    for (let i = 0; i < n; i++)
      parts.push({ x, y, vx: (Math.random() - .5) * v, vy: (Math.random() - .5) * v, l: 1, d: .03,
        h: hues[(Math.random() * 3) | 0] + Math.random() * 25, r: 1.5 });
  }

  /* ---------- main loop ---------- */
  function frame(now) {
    const dt = Math.min((now - last) / 1000, .05); last = now;
    speed += ((chaos ? 4.5 : base) - speed) * Math.min(dt * 3, 1);
    t += dt * speed; sv *= .92;
    rho = chaos ? 34 + 6 * Math.sin(t * 1.7) : 28 + Math.min(sv, 60) * .15;
    document.documentElement.style.setProperty('--sv', Math.min(sv / 50, 1).toFixed(3));

    c.globalCompositeOperation = 'source-over';
    c.fillStyle = `rgba(6,10,26,${chaos ? .06 : .1})`; c.fillRect(0, 0, W, H);
    c.globalCompositeOperation = 'lighter';

    // Lorenz: rotated, projected, pushed away by cursor
    const ang = t * .12 + scrollY * .0013 + nx * .5, ca = Math.cos(ang), sa = Math.sin(ang);
    const s = Math.min(W / 45, H / 55) * 1.15, cx = W * (W > 800 ? .62 : .5) + nx * 20, cy = H * .56;
    const steps = Math.max(1, Math.round(3 * speed));
    c.lineWidth = chaos ? 2 : 1.4; c.lineCap = 'round';
    tr.forEach((p, i) => {
      c.strokeStyle = `hsla(${chaos ? (t * 120 + i * 40) % 360 : 185 + i * (125 / (N - 1))},100%,60%,.85)`;
      c.beginPath();
      let sx, sy;
      for (let k = 0; k < steps; k++) {
        lor(p, .006, rho);
        const X = p.x * ca + p.y * sa, D = -p.x * sa + p.y * ca, z = p.z - 25;
        sx = cx + X * s; sy = cy - (z * .9 + D * .35) * s;
        const dx = sx - mx, dy = sy - my, d = Math.hypot(dx, dy);
        if (d < 140 && d > 0) { const q = (1 - d / 140) * 40; sx += dx / d * q; sy += dy / d * q; }
        if (p.px === null) { p.px = sx; p.py = sy; }
        c.moveTo(p.px, p.py); c.lineTo(sx, sy); p.px = sx; p.py = sy;
      }
      c.stroke();
      c.fillStyle = '#fff'; c.beginPath(); c.arc(sx, sy, chaos ? 3.5 : 2.4, 0, 6.283); c.fill();
    });

    // flowing random-wave particles
    for (const q of ps) {
      const a = (Math.sin(q.x * .004 + t * .5) + Math.cos(q.y * .005 - t * .4)) * Math.PI + (chaos ? Math.sin(t * 5 + q.k) * 2 : 0);
      q.x += Math.cos(a) * q.v * speed * 1.2 + (Math.random() - .5) * sv * .15;
      q.y += Math.sin(a) * q.v * speed * 1.2 + (Math.random() - .5) * sv * .15;
      const dx = q.x - mx, dy = q.y - my, d = Math.hypot(dx, dy);
      if (d < 130 && d > 0) { const m = (1 - d / 130) * 6; q.x += dx / d * m; q.y += dy / d * m; }
      if (q.x < 0) q.x = W; else if (q.x > W) q.x = 0;
      if (q.y < 0) q.y = H; else if (q.y > H) q.y = 0;
      c.fillStyle = `hsla(${chaos ? (t * 90 + q.k * 60) % 360 : q.h},100%,70%,.55)`;
      c.fillRect(q.x, q.y, 1.6, 1.6);
    }

    // scroll turbulence: particles scatter across the screen
    if (sv > 25 && Math.random() < .6) trail(Math.random() * W, Math.random() * H, 6, 6);

    // FX layer
    f.clearRect(0, 0, W, H); f.globalCompositeOperation = 'lighter';
    for (let i = parts.length - 1; i >= 0; i--) {
      const p = parts[i];
      p.x += p.vx; p.y += p.vy; p.vx *= .97; p.vy = p.vy * .97 + .05; p.l -= p.d;
      if (p.l <= 0) { parts[i] = parts[parts.length - 1]; parts.pop(); continue; }
      f.fillStyle = `hsla(${p.h},100%,60%,${p.l})`;
      f.beginPath(); f.arc(p.x, p.y, p.r * (.5 + p.l), 0, 6.283); f.fill();
    }
    requestAnimationFrame(frame);
  }
  requestAnimationFrame(frame);

  /* ---------- input ---------- */
  addEventListener('pointermove', e => {
    mx = e.clientX; my = e.clientY; nx = (mx / W - .5) * 2;
    if (!reduce) trail(mx, my, chaos ? 4 : 2, chaos ? 7 : 2);
  });
  document.addEventListener('pointerleave', () => { mx = my = -999; });
  addEventListener('pointerdown', e => burst(e.clientX, e.clientY, 18, .5));
  addEventListener('scroll', () => { sv = Math.min(sv + Math.abs(scrollY - lastY), 120); lastY = scrollY; }, { passive: true });

  /* ---------- 3D tilt cards ---------- */
  document.querySelectorAll('[data-tilt]').forEach(el => {
    el.addEventListener('pointermove', e => {
      if (e.pointerType === 'touch') return;
      const r = el.getBoundingClientRect(), px = (e.clientX - r.left) / r.width, py = (e.clientY - r.top) / r.height;
      el.style.setProperty('--rx', ((.5 - py) * 16).toFixed(2) + 'deg');
      el.style.setProperty('--ry', ((px - .5) * 16).toFixed(2) + 'deg');
      el.style.setProperty('--mx', px * 100 + '%'); el.style.setProperty('--my', py * 100 + '%');
    });
    el.addEventListener('pointerleave', () => { el.style.setProperty('--rx', '0deg'); el.style.setProperty('--ry', '0deg'); });
  });

  /* ---------- chaos mode ---------- */
  const btn = $('#chaosBtn'), toastEl = $('#toast'), main = $('#main');
  let toastTimer;
  function toast(msg) {
    toastEl.textContent = msg; toastEl.classList.add('show');
    clearTimeout(toastTimer); toastTimer = setTimeout(() => toastEl.classList.remove('show'), 2400);
  }
  function setChaos(on) {
    chaos = on; document.body.classList.toggle('chaos', on);
    btn.setAttribute('aria-pressed', on); btn.textContent = 'Chaos mode: ' + (on ? 'ON' : 'OFF');
    const r = btn.getBoundingClientRect(); burst(r.left + r.width / 2, r.top + r.height / 2, on ? 120 : 40, .8);
  }
  btn.addEventListener('click', () => setChaos(!chaos));

  /* ---------- easter eggs ---------- */
  function unleash() {
    toast('CHAOS UNLEASHED');
    main.classList.remove('shake'); void main.offsetWidth; main.classList.add('shake');
    for (let i = 0; i < 4; i++) setTimeout(() => burst(W * (.2 + Math.random() * .6), H * (.2 + Math.random() * .6), 260, 1.2), i * 160);
  }
  const konami = ['arrowup','arrowup','arrowdown','arrowdown','arrowleft','arrowright','arrowleft','arrowright','b','a'];
  let keys = [];
  addEventListener('keydown', e => {
    keys.push(e.key.toLowerCase()); keys = keys.slice(-10);
    if (keys.slice(-5).join('') === 'chaos' || keys.join() === konami.join()) { keys = []; unleash(); }
  });
  $('#logo').addEventListener('dblclick', e => {
    const r = e.currentTarget.getBoundingClientRect();
    burst(r.left + r.width / 2, r.top + r.height / 2, 400, 1.3); toast('Logo detonated');
  });

  /* ---------- live readout ---------- */
  const ro = $('#readout');
  setInterval(() => { ro.textContent = `σ 10 / ρ ${rho.toFixed(1)} / β 2.67 / ${N} trajectories / speed ×${speed.toFixed(1)}`; }, 120);
})();
</script>
</body>
</html>
