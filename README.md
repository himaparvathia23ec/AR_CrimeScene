<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>AR/VR Crime Scene Memory Distortion Simulator</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Share+Tech+Mono&family=Inter:wght@300;400;500;600&display=swap');

    :root {
      --neon-cyan: #00f5ff;
      --neon-purple: #b400ff;
      --neon-pink: #ff0080;
      --neon-green: #00ff88;
      --dark-bg: #03050f;
      --card-bg: #080d1a;
      --border: rgba(0,245,255,0.2);
    }

    * { margin: 0; padding: 0; box-sizing: border-box; }

    body {
      background: var(--dark-bg);
      color: #c9d6e3;
      font-family: 'Inter', sans-serif;
      line-height: 1.6;
      overflow-x: hidden;
    }

    /* ── GRID BACKGROUND ── */
    body::before {
      content: '';
      position: fixed;
      inset: 0;
      background-image:
        linear-gradient(rgba(0,245,255,0.03) 1px, transparent 1px),
        linear-gradient(90deg, rgba(0,245,255,0.03) 1px, transparent 1px);
      background-size: 40px 40px;
      pointer-events: none;
      z-index: 0;
    }

    .container { max-width: 960px; margin: 0 auto; padding: 0 24px; position: relative; z-index: 1; }

    /* ── HERO ── */
    .hero {
      text-align: center;
      padding: 80px 24px 60px;
      position: relative;
    }

    .hero-glow {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 600px;
      height: 300px;
      background: radial-gradient(ellipse, rgba(180,0,255,0.12) 0%, transparent 70%);
      pointer-events: none;
    }

    .hero-icon {
      font-size: 64px;
      margin-bottom: 20px;
      display: block;
      filter: drop-shadow(0 0 20px var(--neon-cyan));
    }

    .badge-row {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 8px;
      margin-bottom: 28px;
    }

    .badge {
      background: rgba(0,245,255,0.08);
      border: 1px solid rgba(0,245,255,0.3);
      color: var(--neon-cyan);
      font-family: 'Share Tech Mono', monospace;
      font-size: 11px;
      padding: 4px 12px;
      border-radius: 20px;
      letter-spacing: 0.05em;
    }

    .badge.purple { border-color: rgba(180,0,255,0.4); color: #cc66ff; background: rgba(180,0,255,0.08); }
    .badge.pink   { border-color: rgba(255,0,128,0.4); color: #ff66aa; background: rgba(255,0,128,0.08); }
    .badge.green  { border-color: rgba(0,255,136,0.4); color: var(--neon-green); background: rgba(0,255,136,0.08); }

    h1 {
      font-family: 'Orbitron', sans-serif;
      font-size: clamp(24px, 5vw, 42px);
      font-weight: 900;
      line-height: 1.15;
      background: linear-gradient(135deg, var(--neon-cyan) 0%, var(--neon-purple) 50%, var(--neon-pink) 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
      margin-bottom: 16px;
      letter-spacing: 0.02em;
    }

    .tagline {
      font-size: 16px;
      color: rgba(201,214,227,0.65);
      max-width: 580px;
      margin: 0 auto 36px;
      font-weight: 300;
    }

    /* ── SECTION HEADINGS ── */
    .section { padding: 48px 0; }

    h2 {
      font-family: 'Orbitron', sans-serif;
      font-size: 18px;
      font-weight: 700;
      color: var(--neon-cyan);
      letter-spacing: 0.08em;
      text-transform: uppercase;
      margin-bottom: 24px;
      display: flex;
      align-items: center;
      gap: 12px;
    }

    h2::after {
      content: '';
      flex: 1;
      height: 1px;
      background: linear-gradient(90deg, rgba(0,245,255,0.3), transparent);
    }

    h3 {
      font-family: 'Orbitron', sans-serif;
      font-size: 14px;
      font-weight: 700;
      color: #cc66ff;
      letter-spacing: 0.05em;
      text-transform: uppercase;
      margin-bottom: 10px;
    }

    /* ── CARDS ── */
    .card {
      background: var(--card-bg);
      border: 1px solid var(--border);
      border-radius: 12px;
      padding: 24px;
      position: relative;
      overflow: hidden;
    }

    .card::before {
      content: '';
      position: absolute;
      top: 0; left: 0; right: 0;
      height: 2px;
      background: linear-gradient(90deg, transparent, var(--neon-cyan), transparent);
      opacity: 0.5;
    }

    .card.purple-top::before { background: linear-gradient(90deg, transparent, #cc66ff, transparent); }
    .card.pink-top::before   { background: linear-gradient(90deg, transparent, var(--neon-pink), transparent); }
    .card.green-top::before  { background: linear-gradient(90deg, transparent, var(--neon-green), transparent); }

    .grid-2 { display: grid; grid-template-columns: repeat(auto-fit, minmax(240px, 1fr)); gap: 16px; }
    .grid-3 { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 16px; }

    /* ── METRICS ── */
    .metric-card {
      background: var(--card-bg);
      border: 1px solid var(--border);
      border-radius: 12px;
      padding: 28px 20px;
      text-align: center;
    }

    .metric-value {
      font-family: 'Orbitron', sans-serif;
      font-size: 28px;
      font-weight: 900;
      color: var(--neon-cyan);
      display: block;
      margin-bottom: 6px;
    }

    .metric-value.purple { color: #cc66ff; }
    .metric-value.pink   { color: var(--neon-pink); }

    .metric-label {
      font-size: 12px;
      color: rgba(201,214,227,0.55);
      text-transform: uppercase;
      letter-spacing: 0.08em;
      font-family: 'Share Tech Mono', monospace;
    }

    .metric-desc {
      font-size: 11px;
      color: rgba(201,214,227,0.35);
      margin-top: 8px;
      font-family: 'Share Tech Mono', monospace;
    }

    /* ── PROBLEM / SOLUTION ITEMS ── */
    .list-item {
      display: flex;
      align-items: flex-start;
      gap: 12px;
      padding: 10px 0;
      border-bottom: 1px solid rgba(0,245,255,0.06);
    }

    .list-item:last-child { border-bottom: none; }

    .dot {
      width: 8px; height: 8px;
      border-radius: 50%;
      background: var(--neon-cyan);
      margin-top: 7px;
      flex-shrink: 0;
      box-shadow: 0 0 8px var(--neon-cyan);
    }
    .dot.purple { background: #cc66ff; box-shadow: 0 0 8px #cc66ff; }
    .dot.pink   { background: var(--neon-pink); box-shadow: 0 0 8px var(--neon-pink); }
    .dot.green  { background: var(--neon-green); box-shadow: 0 0 8px var(--neon-green); }

    /* ── WORKFLOW STEPS ── */
    .workflow {
      display: flex;
      flex-direction: column;
      gap: 0;
      position: relative;
    }

    .workflow::before {
      content: '';
      position: absolute;
      left: 20px;
      top: 0; bottom: 0;
      width: 1px;
      background: linear-gradient(180deg, var(--neon-cyan), var(--neon-purple), var(--neon-pink));
      opacity: 0.4;
    }

    .step {
      display: flex;
      align-items: flex-start;
      gap: 20px;
      padding: 14px 0;
      position: relative;
    }

    .step-num {
      width: 40px; height: 40px;
      border-radius: 50%;
      background: var(--card-bg);
      border: 1px solid var(--neon-cyan);
      display: flex; align-items: center; justify-content: center;
      font-family: 'Orbitron', sans-serif;
      font-size: 13px;
      font-weight: 700;
      color: var(--neon-cyan);
      flex-shrink: 0;
      box-shadow: 0 0 12px rgba(0,245,255,0.2);
      z-index: 1;
    }

    .step-content strong {
      display: block;
      font-size: 14px;
      font-weight: 600;
      color: #e8eef5;
      margin-bottom: 2px;
    }

    .step-content span {
      font-size: 13px;
      color: rgba(201,214,227,0.5);
    }

    /* ── TECH STACK ── */
    .tech-pill {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      background: rgba(0,245,255,0.06);
      border: 1px solid rgba(0,245,255,0.18);
      border-radius: 8px;
      padding: 8px 14px;
      font-size: 13px;
      font-family: 'Share Tech Mono', monospace;
      color: #c9d6e3;
      margin: 4px;
    }

    .tech-pill .icon { font-size: 16px; }

    /* ── ARCHITECTURE ── */
    .arch-flow {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 0;
    }

    .arch-node {
      background: linear-gradient(135deg, rgba(0,245,255,0.08), rgba(180,0,255,0.08));
      border: 1px solid rgba(0,245,255,0.25);
      border-radius: 10px;
      padding: 14px 32px;
      font-family: 'Share Tech Mono', monospace;
      font-size: 13px;
      color: var(--neon-cyan);
      text-align: center;
      min-width: 200px;
      position: relative;
    }

    .arch-arrow {
      color: rgba(0,245,255,0.4);
      font-size: 20px;
      line-height: 1;
      padding: 4px 0;
    }

    /* ── TEAM ── */
    .team-grid { display: flex; flex-wrap: wrap; gap: 12px; }

    .team-card {
      background: var(--card-bg);
      border: 1px solid rgba(180,0,255,0.25);
      border-radius: 12px;
      padding: 20px 24px;
      text-align: center;
      min-width: 140px;
      flex: 1;
    }

    .avatar {
      width: 52px; height: 52px;
      border-radius: 50%;
      background: linear-gradient(135deg, var(--neon-cyan), var(--neon-purple));
      display: flex; align-items: center; justify-content: center;
      font-family: 'Orbitron', sans-serif;
      font-size: 18px;
      font-weight: 900;
      color: #03050f;
      margin: 0 auto 10px;
    }

    .team-name {
      font-size: 14px;
      font-weight: 600;
      color: #e8eef5;
    }

    /* ── CODE ── */
    pre {
      background: rgba(0,0,0,0.5);
      border: 1px solid rgba(0,245,255,0.12);
      border-radius: 8px;
      padding: 16px 20px;
      font-family: 'Share Tech Mono', monospace;
      font-size: 12.5px;
      color: var(--neon-green);
      overflow-x: auto;
      margin: 10px 0;
    }

    pre .comment { color: rgba(0,255,136,0.4); }

    /* ── FUTURE ── */
    .future-item {
      display: flex;
      align-items: center;
      gap: 14px;
      padding: 12px 16px;
      background: rgba(0,0,0,0.3);
      border: 1px solid rgba(180,0,255,0.12);
      border-radius: 8px;
      margin-bottom: 8px;
      font-size: 14px;
    }

    .future-icon { font-size: 20px; }

    /* ── FOOTER ── */
    footer {
      border-top: 1px solid rgba(0,245,255,0.1);
      padding: 40px 24px;
      text-align: center;
    }

    .footer-title {
      font-family: 'Orbitron', sans-serif;
      font-size: 14px;
      color: rgba(201,214,227,0.4);
      letter-spacing: 0.1em;
      margin-bottom: 12px;
    }

    .footer-sub {
      font-size: 13px;
      color: rgba(201,214,227,0.25);
    }

    /* ── DIVIDER ── */
    .divider {
      height: 1px;
      background: linear-gradient(90deg, transparent, rgba(0,245,255,0.15), transparent);
      margin: 8px 0;
    }

    p { font-size: 14.5px; color: rgba(201,214,227,0.75); }

    @media (max-width: 600px) {
      .workflow::before { left: 16px; }
      .step-num { width: 32px; height: 32px; font-size: 11px; }
      .arch-node { min-width: 160px; padding: 12px 20px; }
    }
  </style>
</head>
<body>

<!-- ═══ HERO ═══ -->
<div class="hero">
  <div class="hero-glow"></div>
  <span class="hero-icon">🥽</span>

  <div class="badge-row">
    <span class="badge">AR/VR</span>
    <span class="badge purple">Unity</span>
    <span class="badge pink">FastAPI</span>
    <span class="badge green">AI-Powered</span>
    <span class="badge">MongoDB</span>
    <span class="badge purple">Cognitive Science</span>
    <span class="badge pink">Forensic Psychology</span>
  </div>

  <h1>AR/VR Crime Scene<br/>Memory Distortion Simulator</h1>

  <p class="tagline">
    An immersive AI-powered system that places you inside a 3D crime scene, then measures
    how accurately — and how honestly — your memory holds up.
  </p>
</div>

<!-- ═══ OVERVIEW ═══ -->
<div class="container">

  <div class="section">
    <h2>🔬 Overview</h2>
    <div class="card">
      <p>
        This project simulates an immersive 3D crime scene where users observe environmental details and later answer
        structured recall questions. An AI analysis engine measures three cognitive dimensions in real time —
        producing a personalised <strong style="color:var(--neon-cyan)">Memory Stability Report</strong> for each session.
      </p>
    </div>
  </div>

  <!-- ═══ KEY METRICS ═══ -->
  <div class="section" style="padding-top:0">
    <h2>📊 Key Metrics</h2>
    <div class="grid-3">
      <div class="metric-card">
        <span class="metric-value">⚡</span>
        <div class="metric-label">Memory Accuracy</div>
        <div class="metric-desc">correct / total questions</div>
      </div>
      <div class="metric-card">
        <span class="metric-value purple">🌀</span>
        <div class="metric-label">Suggestibility Index</div>
        <div class="metric-desc">false memories / total questions</div>
      </div>
      <div class="metric-card">
        <span class="metric-value pink">🧠</span>
        <div class="metric-label">Memory Stability</div>
        <div class="metric-desc">Low · Moderate · High</div>
      </div>
    </div>
  </div>

  <!-- ═══ PROBLEM ═══ -->
  <div class="section">
    <h2>⚠️ Problem Statement</h2>
    <div class="card pink-top">
      <p style="margin-bottom:16px">Human memory is unreliable under stress. Eyewitnesses can:</p>
      <div class="list-item"><div class="dot pink"></div><span>Forget critical scene details during high-stress observation</span></div>
      <div class="list-item"><div class="dot pink"></div><span>Reconstruct false memories influenced by misleading cues</span></div>
      <div class="list-item"><div class="dot pink"></div><span>Overwrite accurate recollections with post-event information</span></div>
    </div>
  </div>

  <!-- ═══ SOLUTION ═══ -->
  <div class="section">
    <h2>💡 Solution</h2>
    <div class="card purple-top">
      <p style="margin-bottom:16px">A closed-loop experimental pipeline that combines immersive simulation with AI cognition analysis:</p>
      <div class="list-item"><div class="dot purple"></div><span>Immersive 3D crime scene rendered in Unity with gyroscope navigation</span></div>
      <div class="list-item"><div class="dot purple"></div><span>Controlled distraction task to induce natural memory decay</span></div>
      <div class="list-item"><div class="dot purple"></div><span>Scene modification to introduce suggestibility triggers</span></div>
      <div class="list-item"><div class="dot purple"></div><span>AI-driven fuzzy matching, synonym detection &amp; confidence weighting</span></div>
      <div class="list-item"><div class="dot purple"></div><span>Automated Memory Stability Report with quantified distortion metrics</span></div>
    </div>
  </div>

  <!-- ═══ WORKFLOW ═══ -->
  <div class="section">
    <h2>🔄 Experiment Workflow</h2>
    <div class="card" style="padding:28px 32px">
      <div class="workflow">
        <div class="step">
          <div class="step-num">01</div>
          <div class="step-content">
            <strong>Session Initialisation</strong>
            <span>User starts experiment; baseline data recorded</span>
          </div>
        </div>
        <div class="step">
          <div class="step-num">02</div>
          <div class="step-content">
            <strong>Crime Scene Observation</strong>
            <span>25-second immersive AR/VR walkthrough with gyroscope navigation</span>
          </div>
        </div>
        <div class="step">
          <div class="step-num">03</div>
          <div class="step-content">
            <strong>Distraction Task</strong>
            <span>Cognitive interference to simulate realistic memory decay</span>
          </div>
        </div>
        <div class="step">
          <div class="step-num">04</div>
          <div class="step-content">
            <strong>Modified Scene Exposure</strong>
            <span>Altered environment introduces suggestibility triggers</span>
          </div>
        </div>
        <div class="step">
          <div class="step-num">05</div>
          <div class="step-content">
            <strong>Recall Questionnaire</strong>
            <span>Structured questions with response-time tracking</span>
          </div>
        </div>
        <div class="step">
          <div class="step-num">06</div>
          <div class="step-content">
            <strong>AI Analysis</strong>
            <span>Fuzzy matching, synonym detection &amp; confidence weighting</span>
          </div>
        </div>
        <div class="step">
          <div class="step-num">07</div>
          <div class="step-content">
            <strong>Memory Stability Report</strong>
            <span>Full dashboard output with distortion metrics</span>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- ═══ ARCHITECTURE ═══ -->
  <div class="section">
    <h2>🏗️ System Architecture</h2>
    <div class="grid-2" style="align-items:start">
      <div class="card">
        <div class="arch-flow">
          <div class="arch-node">🎮 Unity (Crime Scene)</div>
          <div class="arch-arrow">↓</div>
          <div class="arch-node">📝 User Recall Responses</div>
          <div class="arch-arrow">↓</div>
          <div class="arch-node">⚡ FastAPI Backend</div>
          <div class="arch-arrow">↓</div>
          <div class="arch-node">🗄️ MongoDB Database</div>
          <div class="arch-arrow">↓</div>
          <div class="arch-node">🤖 AI Analyser</div>
          <div class="arch-arrow">↓</div>
          <div class="arch-node">📊 Memory Report</div>
        </div>
      </div>

      <div style="display:flex;flex-direction:column;gap:12px">
        <div class="card">
          <h3>Frontend</h3>
          <div>
            <span class="tech-pill"><span class="icon">🎮</span> Unity (AR/VR)</span>
            <span class="tech-pill"><span class="icon">📱</span> Gyroscope Navigation</span>
          </div>
        </div>
        <div class="card purple-top">
          <h3>Backend</h3>
          <div>
            <span class="tech-pill"><span class="icon">⚡</span> FastAPI (Python)</span>
            <span class="tech-pill"><span class="icon">🍃</span> MongoDB</span>
          </div>
        </div>
        <div class="card green-top">
          <h3>AI / Analysis</h3>
          <div>
            <span class="tech-pill"><span class="icon">🧠</span> Rule-based engine</span>
            <span class="tech-pill"><span class="icon">🔍</span> Fuzzy matching</span>
            <span class="tech-pill"><span class="icon">📖</span> Synonym detection</span>
            <span class="tech-pill"><span class="icon">⏱️</span> Response-time weighting</span>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- ═══ PROJECT STRUCTURE ═══ -->
  <div class="section">
    <h2>📁 Project Structure</h2>
    <div class="card">
<pre>AR_CrimeScene_MemoryTest/
├── backend/
│   ├── api/             <span class="comment"># route handlers</span>
│   ├── ai/              <span class="comment"># analysis engine</span>
│   ├── database/        <span class="comment"># MongoDB helpers</span>
│   ├── models/          <span class="comment"># data schemas</span>
│   └── main.py          <span class="comment"># FastAPI entry point</span>
│
├── CrimeScene1/         <span class="comment"># Unity project</span>
│   ├── Assets/
│   ├── Scenes/
│   └── Scripts/
│
├── dashboard/           <span class="comment"># optional viz layer</span>
└── README.md</pre>
    </div>
  </div>

  <!-- ═══ HOW TO RUN ═══ -->
  <div class="section">
    <h2>▶️ How to Run</h2>
    <div class="grid-2">
      <div class="card">
        <h3>1 — Backend Setup</h3>
<pre>cd backend
python -m venv .venv
.\.venv\Scripts\activate
pip install -r requirements.txt
uvicorn main:app --reload</pre>
        <p style="margin-top:12px;font-size:13px">
          API docs available at <code style="color:var(--neon-cyan);font-family:'Share Tech Mono',monospace">http://127.0.0.1:8000/docs</code>
        </p>
      </div>
      <div class="card purple-top">
        <h3>2 — Unity Scene</h3>
        <div class="list-item"><div class="dot purple"></div><span style="font-size:13px">Open project in Unity Editor</span></div>
        <div class="list-item"><div class="dot purple"></div><span style="font-size:13px">Load the crime scene</span></div>
        <div class="list-item"><div class="dot purple"></div><span style="font-size:13px">Set API URL to backend address</span></div>
        <div class="list-item"><div class="dot purple"></div><span style="font-size:13px">Press Play</span></div>
      </div>
    </div>
  </div>

  <!-- ═══ FUTURE IMPROVEMENTS ═══ -->
  <div class="section">
    <h2>🔮 Future Improvements</h2>
    <div class="card">
      <div class="future-item"><span class="future-icon">📸</span> Full AR integration using live camera feed</div>
      <div class="future-item"><span class="future-icon">🔥</span> Attention heatmaps — real-time user focus tracking</div>
      <div class="future-item"><span class="future-icon">🤖</span> ML-based memory distortion prediction models</div>
      <div class="future-item"><span class="future-icon">👥</span> Multi-user concurrent experiments &amp; comparative analysis</div>
      <div class="future-item"><span class="future-icon">📊</span> Advanced dashboard with longitudinal visualisation</div>
    </div>
  </div>

  <!-- ═══ TEAM ═══ -->
  <div class="section">
    <h2>👥 Team</h2>
    <div class="team-grid">
      <div class="team-card">
        <div class="avatar">H</div>
        <div class="team-name">Hima</div>
      </div>
      <div class="team-card">
        <div class="avatar" style="background:linear-gradient(135deg,var(--neon-purple),var(--neon-pink))">H</div>
        <div class="team-name">Harini</div>
      </div>
      <div class="team-card">
        <div class="avatar" style="background:linear-gradient(135deg,var(--neon-pink),#ff6600)">H</div>
        <div class="team-name">Harshita</div>
      </div>
      <div class="team-card">
        <div class="avatar" style="background:linear-gradient(135deg,var(--neon-green),var(--neon-cyan))">C</div>
        <div class="team-name">Chandana</div>
      </div>
    </div>
  </div>

  <!-- ═══ CONCLUSION ═══ -->
  <div class="section">
    <h2>🏁 Conclusion</h2>
    <div class="card green-top">
      <p>
        This project demonstrates how <strong style="color:var(--neon-cyan)">AI + AR/VR</strong> can be combined
        to rigorously study human cognitive behaviour in high-stakes environments. By quantifying memory distortion
        in controlled simulations, it opens new research avenues in forensic psychology, legal evidence assessment,
        and cognitive science — with direct implications for how eyewitness testimony is understood and evaluated.
      </p>
    </div>
  </div>

</div>

<!-- ═══ FOOTER ═══ -->
<footer>
  <div class="footer-title">AR/VR Crime Scene Memory Distortion Simulator</div>
  <div class="footer-sub">Built with Unity · FastAPI · MongoDB · AI Analysis</div>
</footer>

</body>
</html>
