<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Path of the Radiant Sun · D&D 5e</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Cinzel+Decorative:wght@400;700;900&family=Cinzel:wght@400;500;600;700&family=Crimson+Text:ital,wght@0,400;0,600;1,400;1,600&display=swap" rel="stylesheet">
<style>
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
:root {
  --ember:   #f97316;
  --red:     #dc2626;
  --gold:    #facc15;
  --pale:    #fde68a;
  --deep:    #0a0300;
  --panel:   #0d0400;
  --border:  rgba(249,115,22,0.2);
  --border2: rgba(120,53,15,0.3);
  --text:    #ca8a04;
  --muted:   #92400e;
  --dim:     #78350f;
}
html { scroll-behavior: smooth; }
body { background: var(--deep); color: var(--pale); font-family: 'Crimson Text', Georgia, serif; overflow-x: hidden; }
::-webkit-scrollbar { width: 6px; }
::-webkit-scrollbar-track { background: var(--deep); }
::-webkit-scrollbar-thumb { background: #78350f88; border-radius: 99px; }
::-webkit-scrollbar-thumb:hover { background: var(--ember); }

#particles { position: fixed; inset: 0; pointer-events: none; z-index: 0; }

nav {
  position: fixed; top: 0; left: 0; right: 0; z-index: 100;
  display: flex; align-items: center; justify-content: space-between;
  padding: 16px 40px;
  background: linear-gradient(to bottom, rgba(10,3,0,0.95), transparent);
  backdrop-filter: blur(4px); transition: all 0.4s ease;
}
nav.scrolled { background: rgba(10,3,0,0.97); border-bottom: 1px solid var(--border2); }
.nav-logo { font-family: 'Cinzel Decorative', serif; font-size: 13px; letter-spacing: 2px; color: var(--ember); text-decoration: none; }
.nav-links { display: flex; gap: 32px; list-style: none; }
.nav-links a { font-family: 'Cinzel', serif; font-size: 11px; letter-spacing: 3px; text-transform: uppercase; color: var(--dim); text-decoration: none; transition: color 0.3s ease; }
.nav-links a:hover { color: var(--ember); }

#hero {
  position: relative; z-index: 1; min-height: 100vh;
  display: flex; flex-direction: column; align-items: center; justify-content: center;
  text-align: center; padding: 120px 24px 80px; overflow: hidden;
}
.hero-bg {
  position: absolute; inset: 0;
  background:
    radial-gradient(ellipse 80% 50% at 50% 30%, rgba(220,38,38,0.12) 0%, transparent 65%),
    radial-gradient(ellipse 50% 40% at 50% 20%, rgba(249,115,22,0.1) 0%, transparent 60%),
    linear-gradient(180deg, #0a0300 0%, #050100 100%);
}
.rays { position: absolute; top: 12%; left: 50%; transform: translateX(-50%); width: 600px; height: 600px; pointer-events: none; }
.ray { position: absolute; top: 50%; left: 50%; width: 2px; transform-origin: top center; background: linear-gradient(to bottom, rgba(220,38,38,0.18), transparent); border-radius: 99px; }

.hero-eyebrow { position: relative; z-index: 2; font-family: 'Cinzel', serif; font-size: 11px; letter-spacing: 8px; text-transform: uppercase; color: var(--muted); margin-bottom: 24px; opacity: 0; animation: fadeUp 0.8s 0.2s forwards; }
.hero-sun { position: relative; z-index: 2; font-size: 90px; line-height: 1; filter: drop-shadow(0 0 60px #f97316cc); margin-bottom: 28px; display: block; opacity: 0; animation: fadeUp 0.8s 0.4s forwards, slowspin 40s linear 0.8s infinite; animation-fill-mode: forwards; transition: filter 0.8s ease; }
.hero-sun.theone { animation: blaze 1.5s ease-in-out infinite !important; filter: drop-shadow(0 0 80px #fff) drop-shadow(0 0 40px #f97316) !important; }
h1.hero-title { position: relative; z-index: 2; font-family: 'Cinzel Decorative', serif; font-size: clamp(26px, 5.5vw, 58px); font-weight: 900; color: var(--ember); text-shadow: 0 0 80px rgba(249,115,22,0.5); letter-spacing: 3px; line-height: 1.2; margin-bottom: 12px; opacity: 0; animation: fadeUp 0.8s 0.6s forwards; transition: color 0.8s ease, text-shadow 0.8s ease; }
.hero-sub { position: relative; z-index: 2; font-family: 'Cinzel', serif; font-size: 13px; letter-spacing: 4px; text-transform: uppercase; color: var(--muted); margin-bottom: 20px; opacity: 0; animation: fadeUp 0.8s 0.8s forwards; }
.hero-tags { position: relative; z-index: 2; display: flex; gap: 10px; justify-content: center; flex-wrap: wrap; margin-bottom: 48px; opacity: 0; animation: fadeUp 0.8s 1s forwards; }
.hero-tag { padding: 6px 16px; border: 1px solid var(--border2); border-radius: 99px; font-family: 'Cinzel', serif; font-size: 10px; letter-spacing: 3px; text-transform: uppercase; color: var(--dim); background: rgba(249,115,22,0.06); }
.hero-quote { position: relative; z-index: 2; font-style: italic; font-size: 18px; color: var(--muted); max-width: 540px; line-height: 1.7; opacity: 0; animation: fadeUp 0.8s 1.2s forwards; }
.hero-scroll { position: absolute; bottom: 36px; left: 50%; transform: translateX(-50%); z-index: 2; display: flex; flex-direction: column; align-items: center; gap: 8px; opacity: 0; animation: fadeUp 0.8s 1.6s forwards; }
.hero-scroll span { font-family: 'Cinzel', serif; font-size: 9px; letter-spacing: 4px; text-transform: uppercase; color: var(--dim); }
.scroll-line { width: 1px; height: 40px; background: linear-gradient(to bottom, var(--dim), transparent); animation: scrollpulse 2s ease-in-out infinite; }

.section { position: relative; z-index: 1; max-width: 820px; margin: 0 auto; padding: 80px 32px; }
.section-title { font-family: 'Cinzel', serif; font-size: 11px; letter-spacing: 6px; text-transform: uppercase; color: var(--muted); margin-bottom: 40px; display: flex; align-items: center; gap: 20px; }
.section-title::before, .section-title::after { content: ''; flex: 1; height: 1px; background: linear-gradient(to right, transparent, var(--border2)); }
.section-title::after { background: linear-gradient(to left, transparent, var(--border2)); }

.divider { position: relative; z-index: 1; max-width: 820px; margin: 0 auto; padding: 0 32px; display: flex; align-items: center; gap: 20px; }
.divider::before { content: ''; flex: 1; height: 1px; background: linear-gradient(to right, transparent, var(--border2)); }
.divider::after  { content: ''; flex: 1; height: 1px; background: linear-gradient(to left, transparent, var(--border2)); }
.divider-gem { width: 8px; height: 8px; background: var(--ember); transform: rotate(45deg); flex-shrink: 0; box-shadow: 0 0 12px var(--ember); }

.lore-block { text-align: center; font-size: 18px; line-height: 2; color: var(--muted); font-style: italic; max-width: 620px; margin: 0 auto; border: 1px solid var(--border2); border-radius: 2px; padding: 36px 40px; background: linear-gradient(135deg, rgba(220,38,38,0.04), transparent); position: relative; }
.lore-block::before { content: '✦'; position: absolute; top: 14px; left: 20px; font-size: 12px; color: var(--ember); }
.lore-block::after  { content: '✦'; position: absolute; bottom: 14px; right: 20px; font-size: 12px; color: var(--ember); }

.rage-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 16px; }
.rage-card { background: var(--panel); border: 1px solid var(--border2); border-radius: 2px; padding: 20px 22px; transition: border-color 0.3s ease, box-shadow 0.3s ease; }
.rage-card:hover { border-color: var(--ember); box-shadow: 0 0 20px rgba(249,115,22,0.08); }
.rage-card-icon { font-size: 28px; margin-bottom: 10px; display: block; }
.rage-card-name { font-family: 'Cinzel', serif; font-size: 13px; color: var(--pale); letter-spacing: 1px; margin-bottom: 6px; }
.rage-card-desc { font-size: 15px; color: var(--muted); line-height: 1.65; }

.features { display: flex; flex-direction: column; gap: 2px; }
.feature { border: 1px solid transparent; border-radius: 4px; overflow: hidden; transition: border-color 0.3s ease; }
.feature:hover { border-color: var(--border); }
.feature.open { border-color: rgba(249,115,22,0.4); box-shadow: 0 0 30px rgba(249,115,22,0.07); }
.feature-header { display: flex; align-items: center; gap: 20px; padding: 22px 24px; cursor: pointer; background: var(--panel); transition: background 0.3s ease; user-select: none; }
.feature.open .feature-header, .feature-header:hover { background: #120600; }
.feature-icon { font-size: 24px; flex-shrink: 0; width: 36px; text-align: center; }
.feature-info { flex: 1; }
.feature-name { font-family: 'Cinzel', serif; font-size: 15px; color: var(--pale); letter-spacing: 1px; margin-bottom: 5px; }
.feature-tags { display: flex; gap: 6px; flex-wrap: wrap; }
.ftag { font-family: 'Cinzel', serif; font-size: 9px; padding: 2px 8px; border-radius: 2px; letter-spacing: 2px; text-transform: uppercase; }
.ftag-rage { background: rgba(127,29,29,0.5); color: #fca5a5; border: 1px solid rgba(220,38,38,0.3); }
.ftag-weap { background: rgba(59,31,0,0.6); color: #fdba74; border: 1px solid rgba(249,115,22,0.3); }
.ftag-feat { background: rgba(45,26,46,0.6); color: #e9d5ff; border: 1px solid rgba(192,132,252,0.3); }
.ftag-cap  { background: rgba(45,34,0,0.6); color: #fde68a; border: 1px solid rgba(251,191,36,0.3); }
.ftag-lvl  { background: rgba(120,53,15,0.2); color: var(--dim); border: 1px solid transparent; }
.feature-chevron { color: var(--dim); font-size: 14px; transition: transform 0.35s ease, color 0.3s ease; flex-shrink: 0; }
.feature.open .feature-chevron { transform: rotate(180deg); color: var(--ember); }
.feature-body { display: none; padding: 0 24px 24px 80px; background: #120600; font-size: 16px; line-height: 1.9; color: var(--text); white-space: pre-line; border-top: 1px solid rgba(120,53,15,0.2); }
.feature.open .feature-body { display: block; padding-top: 20px; }

.sim-wrapper { background: var(--panel); border: 1px solid var(--border); border-radius: 4px; padding: 40px; position: relative; overflow: hidden; transition: border-color 0.8s ease, box-shadow 0.8s ease; }
.sim-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 40px; align-items: start; }
.sim-tier-name { font-family: 'Cinzel Decorative', serif; font-size: 28px; font-weight: 700; color: var(--ember); transition: color 0.8s ease, text-shadow 0.8s ease; margin-bottom: 6px; }
.sim-tier-desc { font-style: italic; color: var(--muted); font-size: 15px; line-height: 1.6; margin-bottom: 28px; min-height: 48px; }
.progress-label { display: flex; justify-content: space-between; font-family: 'Cinzel', serif; font-size: 11px; letter-spacing: 3px; text-transform: uppercase; color: var(--dim); margin-bottom: 10px; }
.progress-track { height: 8px; background: rgba(28,6,0,0.8); border-radius: 99px; overflow: hidden; border: 1px solid rgba(120,53,15,0.3); margin-bottom: 12px; }
.progress-fill { height: 100%; width: 0%; background: linear-gradient(90deg, #991b1b, var(--ember)); border-radius: 99px; transition: width 0.5s ease, background 0.8s ease; }
.pip-row { display: flex; gap: 6px; margin-bottom: 28px; }
.pip { flex: 1; height: 4px; border-radius: 99px; background: rgba(28,6,0,0.8); border: 1px solid rgba(120,53,15,0.2); cursor: pointer; transition: all 0.3s ease; }
.pip.lit { background: var(--ember); border-color: var(--ember); }
.sim-btns { display: flex; gap: 10px; }
.btn-reset { flex: 1; padding: 12px; background: transparent; border: 1px solid var(--border2); border-radius: 2px; color: var(--dim); cursor: pointer; font-family: 'Cinzel', serif; font-size: 10px; letter-spacing: 3px; text-transform: uppercase; transition: all 0.3s ease; }
.btn-reset:hover { border-color: var(--ember); color: var(--ember); }
.btn-pm { width: 48px; padding: 12px; background: transparent; border: 1px solid var(--border2); border-radius: 2px; color: var(--gold); cursor: pointer; font-size: 20px; transition: all 0.3s ease; }
.btn-pm:hover { border-color: var(--ember); background: rgba(249,115,22,0.1); }
.stat-cards { display: grid; grid-template-columns: 1fr; gap: 12px; }
.stat-card { padding: 18px 20px; background: rgba(10,3,0,0.7); border: 1px solid rgba(120,53,15,0.2); border-radius: 2px; transition: border-color 0.6s ease; }
.stat-card-label { font-family: 'Cinzel', serif; font-size: 9px; letter-spacing: 4px; text-transform: uppercase; color: var(--dim); margin-bottom: 8px; }
.stat-card-val { font-family: 'Cinzel Decorative', serif; font-size: 22px; font-weight: 700; color: var(--ember); transition: color 0.6s ease; }
.theone-banner { display: none; margin-top: 28px; padding: 20px 24px; border: 1px solid rgba(255,255,255,0.3); border-radius: 2px; background: rgba(255,255,255,0.04); text-align: center; animation: pulse 2s ease-in-out infinite; }
.theone-banner.visible { display: block; }
.theone-banner-title { font-family: 'Cinzel Decorative', serif; font-size: 14px; letter-spacing: 4px; color: #fff; margin-bottom: 6px; }
.theone-banner-sub { font-size: 14px; color: #d1d5db; font-style: italic; }

.ref-table-wrap { border: 1px solid var(--border2); border-radius: 2px; overflow: hidden; }
.ref-table-head { padding: 16px 24px; background: rgba(18,6,0,0.8); border-bottom: 1px solid var(--border2); font-family: 'Cinzel', serif; font-size: 10px; letter-spacing: 5px; text-transform: uppercase; color: var(--muted); }
table { width: 100%; border-collapse: collapse; }
thead tr { background: rgba(13,4,0,0.8); }
th { padding: 12px 20px; text-align: left; font-family: 'Cinzel', serif; font-size: 9px; letter-spacing: 3px; color: var(--dim); text-transform: uppercase; font-weight: 400; border-bottom: 1px solid var(--border2); }
td { padding: 14px 20px; border-bottom: 1px solid rgba(120,53,15,0.12); }
tr:last-child td { border-bottom: none; }
.td-sp { color: var(--ember); font-weight: 600; font-family: 'Cinzel', serif; }
.td-name { color: var(--pale); font-family: 'Cinzel', serif; font-size: 13px; }
.td-name.theone { color: #fff; }
.td-val { color: var(--text); font-size: 15px; }
.td-when { color: var(--dim); font-family: 'Cinzel', serif; font-size: 11px; }

.compare-wrap { border: 1px solid var(--border2); border-radius: 2px; overflow: hidden; }
.compare-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 2px; background: rgba(120,53,15,0.15); }
.compare-header { padding: 14px 20px; font-family: 'Cinzel', serif; font-size: 11px; letter-spacing: 3px; text-transform: uppercase; text-align: center; color: var(--pale); }
.compare-header.barb { background: rgba(127,29,29,0.5); }
.compare-header.pala { background: rgba(30,58,95,0.5); }
.compare-row-b { padding: 13px 20px; font-size: 14px; color: var(--muted); line-height: 1.5; background: rgba(127,29,29,0.08); }
.compare-row-p { padding: 13px 20px; font-size: 14px; color: var(--muted); line-height: 1.5; background: rgba(30,58,95,0.08); }
.compare-row-b strong, .compare-row-p strong { color: var(--pale); }

.balance-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }
.balance-item { padding: 18px 20px; background: var(--panel); border: 1px solid var(--border2); border-radius: 2px; font-size: 15px; color: var(--muted); line-height: 1.6; position: relative; padding-left: 32px; }
.balance-item::before { content: '·'; position: absolute; left: 16px; top: 17px; color: var(--ember); font-size: 20px; line-height: 1; }
.hl { color: var(--gold); font-weight: 600; }

footer { position: relative; z-index: 1; text-align: center; padding: 64px 32px; border-top: 1px solid var(--border2); }
.footer-quote { font-family: 'Crimson Text', serif; font-style: italic; font-size: 22px; color: var(--muted); margin-bottom: 12px; }
.footer-attr { font-family: 'Cinzel', serif; font-size: 10px; letter-spacing: 4px; text-transform: uppercase; color: var(--dim); }

@keyframes fadeUp { from { opacity: 0; transform: translateY(24px); } to { opacity: 1; transform: translateY(0); } }
@keyframes slowspin { from { transform: rotate(0deg); } to { transform: rotate(360deg); } }
@keyframes blaze { 0%,100% { filter: drop-shadow(0 0 60px #fff) drop-shadow(0 0 100px #f97316); transform: scale(1); } 50% { filter: drop-shadow(0 0 100px #fff) drop-shadow(0 0 140px #fde68a); transform: scale(1.08); } }
@keyframes pulse { 0%,100% { opacity: 1; } 50% { opacity: 0.5; } }
@keyframes scrollpulse { 0%,100% { opacity: 0.3; } 50% { opacity: 1; } }
.reveal { opacity: 0; transform: translateY(32px); transition: opacity 0.7s ease, transform 0.7s ease; }
.reveal.visible { opacity: 1; transform: none; }

@media (max-width: 700px) {
  nav { padding: 14px 20px; } .nav-links { display: none; }
  .section { padding: 60px 20px; }
  .sim-grid, .balance-grid, .rage-grid, .compare-grid { grid-template-columns: 1fr; }
  .feature-body { padding-left: 24px; } .sim-wrapper { padding: 24px 20px; }
}
</style>
</head>
<body>

<canvas id="particles"></canvas>

<nav id="navbar">
  <a href="#hero" class="nav-logo">☀ Radiant Sun</a>
  <ul class="nav-links">
    <li><a href="#features">Features</a></li>
    <li><a href="#simulator">Simulator</a></li>
    <li><a href="#compare">vs Paladin</a></li>
    <li><a href="#balance">Balance</a></li>
  </ul>
</nav>

<section id="hero">
  <div class="hero-bg"></div>
  <div class="rays" id="raysContainer"></div>
  <p class="hero-eyebrow">Barbarian Subclass · D&D 5e Homebrew</p>
  <span class="hero-sun" id="heroSun">☀</span>
  <h1 class="hero-title" id="mainTitle">Path of the<br>Radiant Sun</h1>
  <p class="hero-sub">The Sin of Pride · Escanor · The Seven Deadly Sins</p>
  <div class="hero-tags">
    <span class="hero-tag">Strength</span>
    <span class="hero-tag">Fire Damage</span>
    <span class="hero-tag">Solar Points</span>
    <span class="hero-tag">Pride</span>
  </div>
  <p class="hero-quote">Some are born with the gifts of gods.<br>You were born with the Sun itself.</p>
  <div class="hero-scroll"><span>Scroll</span><div class="scroll-line"></div></div>
</section>

<div class="section reveal" style="padding-top:40px;padding-bottom:40px;">
  <div class="lore-block">
    With every moment of battle you bloom —<br>
    until no force in the world can stand against you.<br>
    Not by choice. By nature.
  </div>
</div>

<div class="divider reveal"><div class="divider-gem"></div></div>

<section class="section reveal">
  <div class="section-title">What Rage Gives You</div>
  <div class="rage-grid">
    <div class="rage-card"><span class="rage-card-icon">🛡️</span><div class="rage-card-name">Resistance B/P/S</div><div class="rage-card-desc">While raging you already resist bludgeoning, piercing, and slashing — the most common damage types in the game. The One only adds Radiant on top.</div></div>
    <div class="rage-card"><span class="rage-card-icon">💪</span><div class="rage-card-name">Strength Advantage</div><div class="rage-card-desc">Advantage on all Strength checks and saving throws while raging — synergizing directly with Zenith's SP 6–8 bonus.</div></div>
    <div class="rage-card"><span class="rage-card-icon">⚔️</span><div class="rage-card-name">Reckless Attack</div><div class="rage-card-desc">Attack with advantage — and give enemies the same. Escanor never dodged. This is your trigger for the +1 critical SP bonus.</div></div>
    <div class="rage-card"><span class="rage-card-icon">🦴</span><div class="rage-card-name">Unarmored Defense</div><div class="rage-card-desc">CON + DEX to AC with no armor. Escanor wore nothing. His body was the armor. Mechanically identical to his lore.</div></div>
  </div>
</section>

<div class="divider reveal"><div class="divider-gem"></div></div>

<section id="features" class="section reveal">
  <div class="section-title">Subclass Features</div>
  <div class="features" id="featureList"></div>
</section>

<div class="divider reveal"><div class="divider-gem"></div></div>

<section id="simulator" class="section reveal">
  <div class="section-title">Solar Point Simulator</div>
  <div class="sim-wrapper" id="simCard">
    <div class="sim-grid">
      <div>
        <div class="sim-tier-name" id="tierName">Dawn</div>
        <div class="sim-tier-desc" id="tierDesc">The sun rises. Power stirs within.</div>
        <div class="progress-label"><span id="spLabel">SP 0 / 9</span><span>Solar Points</span></div>
        <div class="progress-track"><div class="progress-fill" id="progressFill"></div></div>
        <div class="pip-row" id="pipRow"></div>
        <div class="sim-btns">
          <button class="btn-reset" onclick="setSP(0)">Reset</button>
          <button class="btn-pm" onclick="changeSP(-1)">−</button>
          <button class="btn-pm" onclick="changeSP(1)" id="btnPlus">+</button>
        </div>
        <div class="theone-banner" id="theOneBanner">
          <div class="theone-banner-title">✦ THE ONE AVAILABLE ✦</div>
          <div class="theone-banner-sub">Bonus action · radiant resist · 2d8 fire · +2 melee</div>
        </div>
      </div>
      <div>
        <div class="stat-cards">
          <div class="stat-card"><div class="stat-card-label">Fire Bonus</div><div class="stat-card-val" id="svFire">+1d4</div></div>
          <div class="stat-card"><div class="stat-card-label">Movement Speed</div><div class="stat-card-val" id="svSpeed">—</div></div>
          <div class="stat-card"><div class="stat-card-label">Strength</div><div class="stat-card-val" id="svStr">—</div></div>
        </div>
      </div>
    </div>
  </div>
</section>

<div class="divider reveal"><div class="divider-gem"></div></div>

<div class="section reveal" style="padding-top:0;">
  <div class="ref-table-wrap">
    <div class="ref-table-head">Sun Level Reference</div>
    <table>
      <thead><tr><th>SP</th><th>Level</th><th>Fire</th><th>Speed</th><th>Bonus</th><th>When</th></tr></thead>
      <tbody>
        <tr><td class="td-sp">0–2</td><td class="td-name">Dawn</td><td class="td-val">+1d4</td><td class="td-val">—</td><td class="td-val">—</td><td class="td-when">Round 1</td></tr>
        <tr><td class="td-sp">3–5</td><td class="td-name">Noon</td><td class="td-val">+1d6</td><td class="td-val">+5 ft.</td><td class="td-val">—</td><td class="td-when">Round 2</td></tr>
        <tr><td class="td-sp">6–8</td><td class="td-name">Zenith</td><td class="td-val">+1d8</td><td class="td-val">+10 ft.</td><td class="td-val">STR Advantage</td><td class="td-when">Round 3–4</td></tr>
        <tr style="background:rgba(255,255,255,0.04)"><td class="td-sp">9</td><td class="td-name theone">The One</td><td class="td-val">+2d8</td><td class="td-val">+10 ft.</td><td class="td-val">Adv. + Radiant res.</td><td class="td-when">Round 4–5</td></tr>
      </tbody>
    </table>
  </div>
</div>

<div class="divider reveal"><div class="divider-gem"></div></div>

<section id="compare" class="section reveal">
  <div class="section-title">Barbarian vs Paladin</div>
  <div class="compare-wrap">
    <div class="compare-grid">
      <div class="compare-header barb">☀ Barbarian</div>
      <div class="compare-header pala">✦ Paladin</div>
      <div class="compare-row-b">Trigger: <strong>Rage</strong></div>
      <div class="compare-row-p">Trigger: <strong>Channel Divinity</strong></div>
      <div class="compare-row-b">Damage: <strong>Fire</strong></div>
      <div class="compare-row-p">Damage: <strong>Radiant</strong></div>
      <div class="compare-row-b">SP +1 from: <strong>Critical Hit</strong></div>
      <div class="compare-row-p">SP +1 from: <strong>Divine Smite</strong></div>
      <div class="compare-row-b">The One resist: <strong>Radiant only</strong> (B/P/S from Rage)</div>
      <div class="compare-row-p">The One resist: <strong>ALL types</strong> (no baseline)</div>
      <div class="compare-row-b">The One cost: <strong>1 Exhaustion</strong></div>
      <div class="compare-row-p">The One cost: <strong>2 Exhaustion</strong></div>
      <div class="compare-row-b">Key stat: <strong>Strength / Constitution</strong></div>
      <div class="compare-row-p">Key stat: <strong>Charisma</strong></div>
      <div class="compare-row-b">Fantasy: <strong>Primal solar warrior</strong></div>
      <div class="compare-row-p">Fantasy: <strong>Divine solar knight</strong></div>
    </div>
  </div>
</section>

<div class="divider reveal"><div class="divider-gem"></div></div>

<section id="balance" class="section reveal">
  <div class="section-title">Balance Notes</div>
  <div class="balance-grid">
    <div class="balance-item">SP: +2/round + <span class="hl">+1 on crit</span> — rewards Reckless Attack, The One reachable by round 4–5</div>
    <div class="balance-item">The One: <span class="hl">Radiant resist only</span> — B/P/S already from Rage, zero overlap</div>
    <div class="balance-item">The One: +2 to <span class="hl">melee attacks only</span> — doesn't break damage economy</div>
    <div class="balance-item">Pride of the Lion DC = 8 + prof + <span class="hl">CON</span> — actually useful on a Barbarian</div>
    <div class="balance-item">The One: <span class="hl">1 Exhaustion</span> + 1×/long rest — lower cost than Paladin, no healing option</div>
    <div class="balance-item">Solar Aura: max <span class="hl">9 AOE fire/round</span> — moderate, in line with level 10 features</div>
    <div class="balance-item">Rhitta: <span class="hl">proficiency bonus</span> extra fire — scales naturally, no spike</div>
    <div class="balance-item">Fire (not radiant) — fewer immunities in typical play, balanced trade-off vs Paladin version</div>
  </div>
</section>

<footer>
  <div class="footer-quote">"Who decided that you could stand against me?"</div>
  <div class="footer-attr" style="margin-top:20px;">— Escanor · The Lion's Sin of Pride</div>
  <div class="footer-attr" style="margin-top:10px;color:#78350f55;">Homebrew · D&D 5e · Path of the Radiant Sun</div>
</footer>

<script>
// PARTICLES
const canvas = document.getElementById('particles');
const ctx = canvas.getContext('2d');
let W, H;
function resize() { W = canvas.width = window.innerWidth; H = canvas.height = window.innerHeight; }
resize(); window.addEventListener('resize', resize);
class Particle {
  constructor() { this.reset(); }
  reset() {
    this.x = Math.random()*W; this.y = Math.random()*H;
    this.size = Math.random()*1.8+0.3; this.alpha = Math.random()*0.5+0.05;
    this.vy = -(Math.random()*0.5+0.15); this.vx = (Math.random()-0.5)*0.25;
    this.life = 1; this.decay = Math.random()*0.004+0.001;
    this.color = Math.random()>0.4 ? '#f97316' : Math.random()>0.5 ? '#dc2626' : '#facc15';
  }
  update() { this.x+=this.vx; this.y+=this.vy; this.life-=this.decay; if(this.life<=0||this.y<-10) this.reset(); }
  draw() { ctx.globalAlpha=this.alpha*this.life; ctx.fillStyle=this.color; ctx.beginPath(); ctx.arc(this.x,this.y,this.size,0,Math.PI*2); ctx.fill(); }
}
const particles = Array.from({length:150},()=>new Particle());
function animParticles() { ctx.clearRect(0,0,W,H); particles.forEach(p=>{p.update();p.draw();}); ctx.globalAlpha=1; requestAnimationFrame(animParticles); }
animParticles();

// RAYS
const rc = document.getElementById('raysContainer');
for(let i=0;i<16;i++){const r=document.createElement('div');r.className='ray';r.style.cssText=`transform:rotate(${(i/16)*360}deg) translateX(-50%);opacity:${0.2+Math.random()*0.35};height:${200+Math.random()*140}px;`;rc.appendChild(r);}

// NAV
window.addEventListener('scroll',()=>document.getElementById('navbar').classList.toggle('scrolled',window.scrollY>80));

// REVEAL
const obs = new IntersectionObserver(es=>es.forEach(e=>{if(e.isIntersecting)e.target.classList.add('visible');}),{threshold:0.08});
document.querySelectorAll('.reveal').forEach(el=>obs.observe(el));

// FEATURES
const featuresData = [
  { level:3, tag:"Rage Feature", tagClass:"ftag-rage", icon:"☀️", name:"Sunshine",
    desc:`When you enter a Rage, activate Sunshine and begin tracking Solar Points (SP) from 0 to 9.

Gaining SP during Rage:
• At the start of each of your turns: +2 SP automatically
• When you score a critical hit on that turn: +1 SP additionally
• SP resets to 0 when Rage ends or combat is over

Sun Levels and bonuses to melee attacks:
• SP 0–2 (Dawn): +1d4 fire damage
• SP 3–5 (Noon): +1d6 fire damage, +5 ft. to movement speed
• SP 6–8 (Zenith): +1d8 fire damage, +10 ft. to movement speed, advantage on Strength checks and saving throws
• SP 9 (The One): see level 14 feature

Typical flow: Dawn (round 1) → Noon (round 2) → Zenith (round 3–4) → The One (round 4–5)

Note: Using Reckless Attack increases your chance of critical hits — directly accelerating your Solar Point gain.`
  },
  { level:3, tag:"Sacred Weapon", tagClass:"ftag-weap", icon:"🪓", name:"Sacred Axe — Rhitta",
    desc:`You forge a magical bond with a greataxe or glaive (Rhitta) through a 1-hour ritual. The bond lasts until you perform the ritual with a new weapon. Rhitta gains:

• Extra fire damage equal to your proficiency bonus while you are raging
• Recall: you can summon Rhitta to your hand as a bonus action — it teleports from any distance
• Return: when thrown as a ranged weapon (range 20/60 ft.), it returns to your hand at the end of your turn`
  },
  { level:6, tag:"Feature", tagClass:"ftag-feat", icon:"🦁", name:"Pride of the Lion",
    desc:`Your pride is a shield against weakness:

• You cannot be Frightened while raging.
• When a creature attempts to Frighten you (by any means), it must succeed on a Wisdom saving throw against DC 8 + your proficiency bonus + your Constitution modifier. On a failure, it is Frightened of you for 1 minute. It may repeat the saving throw at the start of each of its turns.
• Once per long rest, when you drop to 0 HP while raging, you may instead drop to 1 HP. Your SP increases by 2.

Note: DC uses Constitution — meaningful on a Barbarian, unlike a Charisma-based DC would be.`
  },
  { level:10, tag:"Feature", tagClass:"ftag-feat", icon:"🌟", name:"Solar Aura",
    desc:`Your body radiates the heat of the sun:

• Bright light fills a 10-foot radius around you. You treat darkness within this radius as dim light.
• At the start of each round, hostile creatures within the aura take fire damage equal to your current SP.
• You gain resistance to fire and radiant damage.
• Your melee attacks count as magical for the purpose of overcoming resistance and immunity.`
  },
  { level:14, tag:"Capstone", tagClass:"ftag-cap", icon:"👑", name:"The One",
    desc:`Once per long rest, when your SP reaches 9, you may activate "The One" as a bonus action for 1 minute (10 rounds):

While The One is active:
• Your SP remains at 9 (it does not reset).
• You double the fire damage die from Sunshine (2d8).
• You gain +2 to all melee attack rolls.
• You gain resistance to radiant damage — the only damage type your Rage does not already cover.
• Once during this form, when you fail a saving throw, you may choose to succeed instead.

When The One ends:
• Your Rage immediately ends.
• You gain 1 level of Exhaustion.

Note: B/P/S resistance is already granted by your Rage — The One only adds Radiant on top. No overlap, no wasted power.

"Who decided that you could stand against me?"`
  },
];
const fl = document.getElementById('featureList');
featuresData.forEach(f=>{
  const div=document.createElement('div'); div.className='feature';
  div.innerHTML=`<div class="feature-header"><div class="feature-icon">${f.icon}</div><div class="feature-info"><div class="feature-name">${f.name}</div><div class="feature-tags"><span class="ftag ${f.tagClass}">${f.tag}</span><span class="ftag ftag-lvl">Level ${f.level}</span></div></div><div class="feature-chevron">▾</div></div><div class="feature-body">${f.desc}</div>`;
  div.querySelector('.feature-header').addEventListener('click',()=>{const o=div.classList.contains('open');document.querySelectorAll('.feature').forEach(el=>el.classList.remove('open'));if(!o)div.classList.add('open');});
  fl.appendChild(div);
});

// SIMULATOR
const tiers=[
  {min:0,max:2,name:"Dawn",   color:"#f97316",glow:"rgba(249,115,22,0.18)",desc:"The sun rises. Power stirs within."},
  {min:3,max:5,name:"Noon",   color:"#facc15",glow:"rgba(250,204,21,0.14)",desc:"The sun climbs high. Warmth becomes fire."},
  {min:6,max:8,name:"Zenith", color:"#fde68a",glow:"rgba(253,230,138,0.12)",desc:"Full solar power washes over the battlefield."},
  {min:9,max:9,name:"The One",color:"#ffffff",glow:"rgba(255,255,255,0.2)", desc:"Who decided that you could stand against me?"},
];
let sp=0;
function getTier(v){return tiers.find(t=>v>=t.min&&v<=t.max);}
const pipRow=document.getElementById('pipRow');
for(let i=0;i<=9;i++){const p=document.createElement('div');p.className='pip';p.addEventListener('click',()=>setSP(i));pipRow.appendChild(p);}
function updateSim(){
  const tier=getTier(sp);
  const sun=document.getElementById('heroSun');
  sun.style.filter=`drop-shadow(0 0 60px ${tier.color})`;
  sun.className='hero-sun'+(sp>=9?' theone':'');
  const title=document.getElementById('mainTitle');
  title.style.color=tier.color;
  title.style.textShadow=`0 0 80px ${tier.color}55`;
  const card=document.getElementById('simCard');
  card.style.borderColor=tier.color+'55';
  card.style.boxShadow=`0 0 60px ${tier.glow}`;
  document.getElementById('tierName').textContent=tier.name;
  document.getElementById('tierName').style.color=tier.color;
  document.getElementById('tierName').style.textShadow=`0 0 30px ${tier.color}66`;
  document.getElementById('tierDesc').textContent=tier.desc;
  document.getElementById('spLabel').textContent=`SP ${sp} / 9`;
  const fill=document.getElementById('progressFill');
  fill.style.width=`${(sp/9)*100}%`;
  fill.style.background=`linear-gradient(90deg, #991b1b, ${tier.color})`;
  document.querySelectorAll('.pip').forEach((p,i)=>{p.classList.toggle('lit',i<=sp);p.style.background=i<=sp?tier.color:'';p.style.borderColor=i<=sp?tier.color:'';});
  document.getElementById('svFire').textContent=sp<=2?'+1d4':sp<=5?'+1d6':sp<=8?'+1d8':'+2d8';
  document.getElementById('svSpeed').textContent=sp<=2?'—':sp<=5?'+5 ft.':'+10 ft.';
  document.getElementById('svStr').textContent=sp<=5?'—':'Advantage';
  ['svFire','svSpeed','svStr'].forEach(id=>document.getElementById(id).style.color=tier.color);
  document.querySelectorAll('.stat-card').forEach(c=>c.style.borderColor=tier.color+'33');
  document.getElementById('btnPlus').style.borderColor=tier.color+'66';
  document.getElementById('btnPlus').style.color=tier.color;
  document.getElementById('theOneBanner').classList.toggle('visible',sp===9);
}
function setSP(v){sp=Math.max(0,Math.min(9,v));updateSim();}
function changeSP(d){setSP(sp+d);}
updateSim();
</script>
</body>
</html>
