<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Netlithic</title>
  <style>
    :root {
      --bg: #040816;
      --bg-2: #081225;
      --panel: rgba(11, 24, 52, 0.72);
      --line: rgba(116, 166, 255, 0.18);
      --text: #eef4ff;
      --muted: #9fb3d9;
      --blue: #5ea2ff;
      --blue-2: #2f7cf6;
      --glow: rgba(94, 162, 255, 0.35);
      --success: #8dd3ff;
      --shadow: 0 20px 60px rgba(0, 0, 0, 0.45);
      --radius: 24px;
      --max: 1180px;
    }

    * { box-sizing: border-box; }
    html { scroll-behavior: smooth; }
    body {
      margin: 0;
      font-family: Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
      color: var(--text);
      background:
        radial-gradient(circle at top, rgba(56, 130, 246, 0.18), transparent 28%),
        radial-gradient(circle at 20% 20%, rgba(94, 162, 255, 0.14), transparent 25%),
        linear-gradient(180deg, #040915 0%, #020611 100%);
      overflow-x: hidden;
    }

    body::before,
    body::after {
      content: "";
      position: fixed;
      inset: auto;
      width: 40vw;
      height: 40vw;
      filter: blur(100px);
      z-index: -2;
      opacity: 0.22;
      pointer-events: none;
    }

    body::before {
      top: -10vw;
      left: -8vw;
      background: #1f6dff;
    }

    body::after {
      bottom: -15vw;
      right: -10vw;
      background: #113c8f;
    }

    .grid-overlay {
      position: fixed;
      inset: 0;
      background-image:
        linear-gradient(rgba(255,255,255,0.03) 1px, transparent 1px),
        linear-gradient(90deg, rgba(255,255,255,0.03) 1px, transparent 1px);
      background-size: 56px 56px;
      mask-image: radial-gradient(circle at center, black 35%, transparent 85%);
      z-index: -1;
      pointer-events: none;
    }

    a { color: inherit; text-decoration: none; }

    .container {
      width: min(calc(100% - 40px), var(--max));
      margin: 0 auto;
    }

    .nav {
      position: sticky;
      top: 0;
      z-index: 50;
      backdrop-filter: blur(18px);
      background: rgba(4, 9, 21, 0.55);
      border-bottom: 1px solid rgba(255,255,255,0.06);
    }

    .nav-inner {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 18px 0;
    }

    .brand {
      display: flex;
      align-items: center;
      gap: 12px;
      font-weight: 800;
      letter-spacing: 0.14em;
      text-transform: uppercase;
    }

    .brand-logo {
      width: 40px;
      height: 40px;
      object-fit: contain;
      filter: drop-shadow(0 0 12px rgba(94,162,255,0.2));
    }

    .nav-links {
      display: flex;
      align-items: center;
      gap: 24px;
      color: var(--muted);
      font-size: 0.95rem;
    }

    .nav-links a:hover { color: var(--text); }

    .nav-cta {
      padding: 12px 18px;
      border-radius: 999px;
      border: 1px solid rgba(116, 166, 255, 0.3);
      background: linear-gradient(180deg, rgba(94,162,255,0.18), rgba(94,162,255,0.08));
      box-shadow: 0 0 24px rgba(94,162,255,0.14);
      font-weight: 600;
    }

    .hero {
      padding: 72px 0 48px;
    }

    .hero-wrap {
      display: grid;
      grid-template-columns: 1.08fr 0.92fr;
      gap: 36px;
      align-items: center;
    }

    .eyebrow {
      display: inline-flex;
      align-items: center;
      gap: 10px;
      padding: 10px 14px;
      border-radius: 999px;
      background: rgba(94,162,255,0.08);
      border: 1px solid rgba(116,166,255,0.18);
      color: var(--success);
      font-size: 0.9rem;
      margin-bottom: 20px;
    }

    .hero h1 {
      margin: 0 0 16px;
      font-size: clamp(2.8rem, 6vw, 5.3rem);
      line-height: 0.96;
      letter-spacing: -0.05em;
      text-transform: uppercase;
    }

    .hero h1 span {
      display: block;
      background: linear-gradient(180deg, #f4f8ff 0%, #74a6ff 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
    }

    .hero p {
      margin: 0 0 28px;
      max-width: 650px;
      color: var(--muted);
      font-size: 1.08rem;
      line-height: 1.7;
    }

    .hero-actions {
      display: flex;
      flex-wrap: wrap;
      gap: 14px;
      margin-bottom: 28px;
    }

    .btn {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: 10px;
      min-height: 52px;
      padding: 0 22px;
      border-radius: 16px;
      border: 1px solid transparent;
      font-weight: 700;
      transition: transform 0.2s ease, box-shadow 0.2s ease, border-color 0.2s ease;
    }

    .btn:hover { transform: translateY(-2px); }

    .btn-primary {
      background: linear-gradient(135deg, var(--blue), var(--blue-2));
      color: white;
      box-shadow: 0 10px 30px var(--glow);
    }

    .btn-secondary {
      color: var(--text);
      background: rgba(255,255,255,0.03);
      border-color: rgba(255,255,255,0.1);
    }

    .hero-stats {
      display: grid;
      grid-template-columns: repeat(3, minmax(0, 1fr));
      gap: 14px;
      max-width: 680px;
    }

    .stat,
    .mini-panel,
    .feature,
    .phase,
    .token-card,
    .builder-card,
    .community-card {
      padding: 18px;
      border-radius: 20px;
      background: rgba(255,255,255,0.03);
      border: 1px solid rgba(255,255,255,0.08);
      box-shadow: var(--shadow);
    }

    .stat strong {
      display: block;
      margin-bottom: 8px;
      font-size: 1.2rem;
    }

    .stat span,
    .mini-panel p,
    .feature p,
    .phase p,
    .token-card p,
    .builder-card p,
    .community-card p,
    .network-row span,
    .status-badges span,
    .arch-node p {
      color: var(--muted);
      font-size: 0.92rem;
      line-height: 1.7;
    }

    .hero-visual {
      position: relative;
    }

    .hero-logo-badge {
      position: absolute;
      top: -18px;
      right: 18px;
      width: 92px;
      height: 92px;
      object-fit: contain;
      padding: 14px;
      border-radius: 24px;
      background: rgba(7, 16, 34, 0.78);
      border: 1px solid rgba(116, 166, 255, 0.18);
      box-shadow: 0 18px 40px rgba(0, 0, 0, 0.32);
      backdrop-filter: blur(18px);
    }

    .hero-card {
      position: relative;
      padding: 28px;
      border-radius: 30px;
      background: linear-gradient(180deg, rgba(13, 26, 58, 0.9), rgba(8, 18, 39, 0.85));
      border: 1px solid var(--line);
      box-shadow: var(--shadow);
      overflow: hidden;
    }

    .hero-card::before {
      content: "";
      position: absolute;
      inset: -30% 0 auto;
      height: 220px;
      background: radial-gradient(circle, rgba(94,162,255,0.18), transparent 70%);
      pointer-events: none;
    }

    .terminal {
      border-radius: 22px;
      border: 1px solid rgba(255,255,255,0.08);
      background: rgba(3, 9, 24, 0.88);
      overflow: hidden;
    }

    .terminal-top {
      display: flex;
      align-items: center;
      gap: 8px;
      padding: 14px 16px;
      border-bottom: 1px solid rgba(255,255,255,0.06);
      background: rgba(255,255,255,0.02);
    }

    .dot {
      width: 10px;
      height: 10px;
      border-radius: 999px;
      background: rgba(255,255,255,0.35);
    }

    .terminal-body {
      padding: 20px;
      font-family: "SFMono-Regular", Consolas, "Liberation Mono", Menlo, monospace;
      font-size: 0.92rem;
      color: #dce9ff;
      line-height: 1.9;
    }

    .token { color: #79b0ff; }
    .comment { color: #7f91b4; }
    .good { color: #87ffc1; }

    .floating-card,
    .mini-grid,
    .token-grid,
    .builder-grid,
    .community-grid,
    .status-grid {
      display: grid;
      gap: 12px;
    }

    .floating-card {
      margin-top: 18px;
      grid-template-columns: repeat(2, 1fr);
    }

    .pill,
    .status-badge {
      padding: 12px 14px;
      border-radius: 16px;
      background: rgba(94,162,255,0.08);
      border: 1px solid rgba(116,166,255,0.12);
      color: var(--muted);
      font-size: 0.9rem;
    }

    .section {
      padding: 42px 0;
    }

    .section-head {
      display: flex;
      justify-content: space-between;
      align-items: end;
      gap: 24px;
      margin-bottom: 22px;
    }

    .section-head h2 {
      margin: 0;
      font-size: clamp(1.8rem, 4vw, 3rem);
      letter-spacing: -0.04em;
    }

    .section-head p {
      margin: 0;
      max-width: 560px;
      color: var(--muted);
      line-height: 1.7;
    }

    .feature-grid,
    .roadmap,
    .token-grid,
    .builder-grid,
    .community-grid {
      display: grid;
      grid-template-columns: repeat(3, minmax(0, 1fr));
      gap: 18px;
    }

    .feature,
    .phase,
    .token-card,
    .builder-card,
    .community-card {
      position: relative;
      padding: 26px;
      overflow: hidden;
    }

    .feature::after,
    .token-card::after,
    .builder-card::after,
    .community-card::after {
      content: "";
      position: absolute;
      inset: 0;
      background: linear-gradient(180deg, rgba(94,162,255,0.06), transparent 45%);
      opacity: 0;
      transition: opacity 0.2s ease;
    }

    .feature:hover::after,
    .token-card:hover::after,
    .builder-card:hover::after,
    .community-card:hover::after { opacity: 1; }

    .feature-icon {
      width: 52px;
      height: 52px;
      display: grid;
      place-items: center;
      border-radius: 18px;
      background: rgba(94,162,255,0.1);
      border: 1px solid rgba(116,166,255,0.16);
      margin-bottom: 18px;
      color: var(--blue);
      font-weight: 800;
    }

    .feature h3,
    .phase h3,
    .token-card h3,
    .builder-card h3,
    .community-card h3,
    .mini-panel h3,
    .network-panel h3,
    .arch-node h3 {
      margin: 0 0 10px;
      font-size: 1.08rem;
    }

    .protocol-layout,
    .network-layout {
      display: grid;
      grid-template-columns: 1.15fr 0.85fr;
      gap: 18px;
      align-items: stretch;
    }

    .protocol-card,
    .network-panel,
    .architecture-card {
      padding: 28px;
      border-radius: 28px;
      background: linear-gradient(180deg, rgba(255,255,255,0.04), rgba(255,255,255,0.02));
      border: 1px solid rgba(255,255,255,0.08);
      box-shadow: var(--shadow);
    }

    .protocol-list,
    .status-list {
      display: grid;
      gap: 14px;
      margin-top: 18px;
    }

    .mini-grid {
      grid-template-columns: repeat(2, 1fr);
      margin-top: 18px;
    }

    .mini-panel strong,
    .network-row strong,
    .status-badges strong {
      display: block;
      margin-bottom: 8px;
      font-size: 1rem;
    }

    .architecture-flow {
      display: grid;
      gap: 14px;
    }

    .arch-node {
      padding: 18px 20px;
      border-radius: 18px;
      background: rgba(94,162,255,0.06);
      border: 1px solid rgba(116,166,255,0.16);
      position: relative;
    }

    .arch-node:not(:last-child)::after {
      content: "↓";
      position: absolute;
      left: 50%;
      transform: translateX(-50%);
      bottom: -18px;
      color: var(--blue);
      font-size: 1.1rem;
    }

    .roadmap {
      grid-template-columns: repeat(4, minmax(0, 1fr));
      gap: 16px;
    }

    .phase small,
    .eyebrow-alt {
      display: inline-block;
      margin-bottom: 12px;
      color: var(--blue);
      text-transform: uppercase;
      letter-spacing: 0.14em;
      font-weight: 700;
      font-size: 0.75rem;
    }

    .token-grid { grid-template-columns: repeat(4, minmax(0, 1fr)); }

    .token-number,
    .community-number {
      display: block;
      margin-bottom: 10px;
      font-size: 2rem;
      font-weight: 800;
      letter-spacing: -0.04em;
      color: var(--text);
    }

    .community-grid { grid-template-columns: repeat(3, minmax(0, 1fr)); }

    .network-panel {
      background: linear-gradient(180deg, rgba(13, 26, 58, 0.85), rgba(8, 18, 39, 0.84));
    }

    .status-grid {
      grid-template-columns: repeat(2, minmax(0, 1fr));
      margin-top: 18px;
    }

    .network-row {
      padding: 16px;
      border-radius: 18px;
      background: rgba(255,255,255,0.03);
      border: 1px solid rgba(255,255,255,0.08);
    }

    .status-badges {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      margin-top: 18px;
    }

    .cta {
      padding: 48px 0 80px;
    }

    .cta-box {
      position: relative;
      padding: 38px;
      border-radius: 32px;
      background: linear-gradient(135deg, rgba(94,162,255,0.14), rgba(8,21,45,0.92));
      border: 1px solid rgba(116,166,255,0.18);
      box-shadow: var(--shadow);
      overflow: hidden;
    }

    .cta-box::before {
      content: "";
      position: absolute;
      inset: auto -10% -60% auto;
      width: 340px;
      height: 340px;
      border-radius: 999px;
      background: radial-gradient(circle, rgba(94,162,255,0.22), transparent 60%);
      pointer-events: none;
    }

    .cta-box h2 {
      margin: 0 0 12px;
      font-size: clamp(2rem, 4vw, 3.2rem);
      letter-spacing: -0.04em;
    }

    .cta-box p {
      margin: 0 0 22px;
      max-width: 720px;
      color: var(--muted);
      line-height: 1.7;
    }

    .footer {
      padding: 24px 0 40px;
      color: var(--muted);
      border-top: 1px solid rgba(255,255,255,0.06);
    }

    .footer-inner {
      display: flex;
      justify-content: space-between;
      gap: 20px;
      flex-wrap: wrap;
    }

    .reveal {
      opacity: 0;
      transform: translateY(24px);
      transition: opacity 0.7s ease, transform 0.7s ease;
    }

    .reveal.visible {
      opacity: 1;
      transform: translateY(0);
    }

    @media (max-width: 1024px) {
      .hero-wrap,
      .protocol-layout,
      .network-layout,
      .feature-grid,
      .roadmap,
      .token-grid,
      .builder-grid,
      .community-grid {
        grid-template-columns: 1fr 1fr;
      }

      .hero-wrap > :first-child,
      .protocol-layout > :first-child,
      .network-layout > :first-child {
        grid-column: span 2;
      }
    }

    @media (max-width: 760px) {
      .nav-links { display: none; }
      .hero { padding-top: 42px; }
      .hero-wrap,
      .protocol-layout,
      .network-layout,
      .feature-grid,
      .roadmap,
      .hero-stats,
      .floating-card,
      .mini-grid,
      .token-grid,
      .builder-grid,
      .community-grid,
      .status-grid {
        grid-template-columns: 1fr;
      }

      .hero-wrap > :first-child,
      .protocol-layout > :first-child,
      .network-layout > :first-child { grid-column: span 1; }

      .section-head,
      .footer-inner {
        flex-direction: column;
        align-items: flex-start;
      }

      .cta-box,
      .hero-card,
      .feature,
      .phase,
      .protocol-card,
      .network-panel,
      .architecture-card,
      .token-card,
      .builder-card,
      .community-card { padding: 24px; }
    }
  </style>
</head>
<body>
  <div class="grid-overlay"></div>

  <header class="nav">
    <div class="container nav-inner">
      <a href="#top" class="brand">
        <img src="assets/netlithic-icon.png" alt="Netlithic logo" class="brand-logo" />
        <span>Netlithic</span>
      </a>

      <nav class="nav-links">
        <a href="#vision">Vision</a>
        <a href="#features">Features</a>
        <a href="#why">Why Netlithic</a>
        <a href="#roadmap">Roadmap</a>
        <a href="https://github.com/IronNode951/Netlithic" target="_blank" rel="noreferrer">GitHub</a>
        <a href="https://x.com/netlithicchain" target="_blank" rel="noreferrer">X</a>
        <a href="https://discord.gg/a92xq4du" target="_blank" rel="noreferrer">Discord</a>
        <a href="#cta" class="nav-cta">Join Early</a>
      </nav>
    </div>
  </header>

  <main id="top">
    <section class="hero">
      <div class="container hero-wrap">
        <div class="reveal visible">
          <div class="eyebrow">⚡ Community-governed. AI-native. Anti-manipulation by design.</div>
          <h1>
            The chain built to
            <span>outgrow meme-cycle chaos.</span>
          </h1>
          <p>
            Netlithic is a next-generation blockchain experiment focused on reducing pump-and-dump dynamics,
            strengthening community governance, and laying the groundwork for AI-native protocols that can actually scale.
          </p>

          <div class="hero-actions">
            <a class="btn btn-primary" href="https://github.com/IronNode951/Netlithic" target="_blank" rel="noreferrer">Explore the build</a>
            <a class="btn btn-secondary" href="#features">See the vision</a>
            <a class="btn btn-secondary" href="https://discord.gg/a92xq4du" target="_blank" rel="noreferrer">Join Discord</a>
          </div>

          <div class="hero-stats">
            <div class="stat">
              <strong>Fair launch direction</strong>
              <span>Built around community-first design instead of hype-driven extraction.</span>
            </div>
            <div class="stat">
              <strong>Governance focus</strong>
              <span>Upgrades, treasury, and growth shaped by aligned participation.</span>
            </div>
            <div class="stat">
              <strong>AI-native future</strong>
              <span>Structured to support protocol tools and onchain agent coordination.</span>
            </div>
          </div>
        </div>

        <div class="hero-visual reveal">
          <img src="assets/netlithic-icon.png" alt="Netlithic icon" class="hero-logo-badge" />
          <div class="hero-card">
          <div class="terminal">
            <div class="terminal-top">
              <div class="dot"></div>
              <div class="dot"></div>
              <div class="dot"></div>
            </div>
            <div class="terminal-body">
              <div><span class="comment">// Netlithic mission</span></div>
              <div><span class="token">consensus</span>: community-aligned</div>
              <div><span class="token">launch</span>: fair and transparent</div>
              <div><span class="token">protection</span>: anti-whale incentives</div>
              <div><span class="token">future</span>: AI-native infrastructure</div>
              <div><span class="good">status</span>: building in public</div>
            </div>
          </div>

          <div class="floating-card">
            <div class="pill">Token design focused on healthier market behavior</div>
            <div class="pill">Governance primitives for long-term alignment</div>
            <div class="pill">Simple, strong launch story for community growth</div>
            <div class="pill">Clean foundation for future protocol expansion</div>
          </div>
        </div>
      </div>
    </section>

    <section class="section" id="vision">
      <div class="container">
        <div class="section-head reveal">
          <div>
            <h2>Built for conviction, not quick flips</h2>
          </div>
          <p>
            Most launches reward timing games, insider exits, and attention spikes. Netlithic aims for the opposite:
            a cleaner launch philosophy, stronger social trust, and a blockchain identity people can actually rally around.
          </p>
        </div>

        <div class="protocol-layout">
          <div class="protocol-card reveal">
            <span class="eyebrow-alt">Protocol</span>
            <h3>The Netlithic Protocol</h3>
            <p>
              Netlithic is a community-governed blockchain concept designed to reduce speculative market manipulation,
              align long-term participation, and create a foundation for AI-native infrastructure.
            </p>
            <div class="protocol-list">
              <div class="mini-panel">
                <strong>Community-first governance</strong>
                <p>Protocol direction, treasury evolution, and upgrades are meant to be shaped by aligned builders over time.</p>
              </div>
              <div class="mini-panel">
                <strong>Anti-extraction philosophy</strong>
                <p>The goal is to discourage short-term attention farming and encourage healthier network behavior from day one.</p>
              </div>
            </div>
            <div class="mini-grid">
              <div class="mini-panel">
                <strong>Open source</strong>
                <p>Built in public with GitHub-native iteration.</p>
              </div>
              <div class="mini-panel">
                <strong>AI-native path</strong>
                <p>Structured for future protocol automation and agent tooling.</p>
              </div>
            </div>
          </div>

          <div class="architecture-card reveal">
            <span class="eyebrow-alt">Architecture</span>
            <h3>System design path</h3>
            <div class="architecture-flow">
              <div class="arch-node">
                <h3>Nodes</h3>
                <p>Independent participants help secure and relay the network.</p>
              </div>
              <div class="arch-node">
                <h3>Consensus Layer</h3>
                <p>Agreement logic keeps state updates coordinated and verifiable.</p>
              </div>
              <div class="arch-node">
                <h3>Governance Layer</h3>
                <p>Community decisions guide treasury, upgrades, and protocol direction.</p>
              </div>
              <div class="arch-node">
                <h3>AI Protocol Layer</h3>
                <p>Future-ready foundation for intelligent agents and onchain automation.</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section class="section" id="features">
      <div class="container">
        <div class="section-head reveal">
          <div>
            <h2>Core pillars</h2>
          </div>
          <p>
            A sharper landing page should explain what makes Netlithic different in seconds. These three pillars do that fast.
          </p>
        </div>

        <div class="feature-grid">
          <article class="feature reveal">
            <div class="feature-icon">01</div>
            <h3>Anti-manipulation design</h3>
            <p>
              Structure incentives to reduce the usual short-term extraction patterns that destroy trust in early-stage communities.
            </p>
          </article>

          <article class="feature reveal">
            <div class="feature-icon">02</div>
            <h3>Community-first governance</h3>
            <p>
              Use transparent decision-making and treasury logic so the project feels owned by its builders, not captured by insiders.
            </p>
          </article>

          <article class="feature reveal">
            <div class="feature-icon">03</div>
            <h3>AI-native protocol path</h3>
            <p>
              Design the brand and architecture from day one for agent tooling, automation layers, and future onchain intelligence.
            </p>
          </article>
        </div>
      </div>
    </section>

    <section class="section" id="why">
      <div class="container">
        <div class="section-head reveal">
          <div>
            <h2>Why Netlithic exists</h2>
          </div>
          <p>
            The crypto space keeps replaying the same cycle: attention spikes, insiders unload, communities fracture, and the mission disappears.
            Netlithic is meant to challenge that pattern with a more durable identity and a stronger launch philosophy.
          </p>
        </div>

        <div class="feature-grid">
          <article class="feature reveal">
            <div class="feature-icon">A</div>
            <h3>Trust is the moat</h3>
            <p>
              A serious chain brand should earn conviction through clarity, transparency, and repeatable community behavior — not pure volatility.
            </p>
          </article>

          <article class="feature reveal">
            <div class="feature-icon">B</div>
            <h3>Utility needs a runway</h3>
            <p>
              Before AI agents and advanced protocol layers can matter, the base community and launch mechanics need to survive first contact with the market.
            </p>
          </article>

          <article class="feature reveal">
            <div class="feature-icon">C</div>
            <h3>Brand shapes belief</h3>
            <p>
              When the site looks premium and the message is sharp, people feel the difference immediately. That first impression matters more than most teams realize.
            </p>
          </article>
        </div>
      </div>
    </section>

    <section class="section" id="roadmap">
      <div class="container">
        <div class="section-head reveal">
          <div>
            <h2>Roadmap</h2>
          </div>
          <p>
            Keep the message simple: launch the idea, grow the community, harden the mechanism, then expand into infrastructure.
          </p>
        </div>

        <div class="roadmap">
          <article class="phase reveal">
            <small>Phase 01</small>
            <h3>Identity + launch story</h3>
            <p>Dial in the website, mission, socials, and public narrative so the brand feels premium from the start.</p>
          </article>

          <article class="phase reveal">
            <small>Phase 02</small>
            <h3>Community formation</h3>
            <p>Bring early believers into Discord, GitHub, and governance conversations around the protocol direction.</p>
          </article>

          <article class="phase reveal">
            <small>Phase 03</small>
            <h3>Mechanism testing</h3>
            <p>Model token behavior, anti-dump protections, and governance incentives before broad market exposure.</p>
          </article>

          <article class="phase reveal">
            <small>Phase 04</small>
            <h3>AI-native expansion</h3>
            <p>Layer in agent tooling, automation, and protocol utilities that give the chain a long-term reason to exist.</p>
          </article>
        </div>
      </div>
    </section>

    <section class="section" id="tokenomics">
      <div class="container">
        <div class="section-head reveal">
          <div>
            <h2>Tokenomics direction</h2>
          </div>
          <p>
            Serious protocols explain how incentives will align. This section signals economic intention, transparency, and long-term planning.
          </p>
        </div>

        <div class="token-grid">
          <article class="token-card reveal">
            <span class="token-number">40%</span>
            <h3>Community treasury</h3>
            <p>Reserved for governance-led growth, grants, ecosystem development, and long-term coordination.</p>
          </article>
          <article class="token-card reveal">
            <span class="token-number">25%</span>
            <h3>Ecosystem development</h3>
            <p>Supports tooling, integrations, protocol utilities, and expansion of the builder surface area.</p>
          </article>
          <article class="token-card reveal">
            <span class="token-number">15%</span>
            <h3>Core contributors</h3>
            <p>Designed to align the people doing the work without making the project feel insider-captured.</p>
          </article>
          <article class="token-card reveal">
            <span class="token-number">20%</span>
            <h3>Reserve + early builders</h3>
            <p>Maintains flexibility for future incentives, strategic growth, and committed early participation.</p>
          </article>
        </div>
      </div>
    </section>

    <section class="section" id="ecosystem">
      <div class="container">
        <div class="section-head reveal">
          <div>
            <h2>Ecosystem vision</h2>
          </div>
          <p>
            Billion-dollar projects do not just explain what they are. They show what can exist on top of them.
          </p>
        </div>

        <div class="builder-grid">
          <article class="builder-card reveal">
            <div class="feature-icon">◎</div>
            <h3>AI agent infrastructure</h3>
            <p>Foundations for autonomous systems that need transparent coordination, execution, and onchain identity.</p>
          </article>
          <article class="builder-card reveal">
            <div class="feature-icon">↗</div>
            <h3>Governance tooling</h3>
            <p>Modules for proposals, treasury coordination, and community participation layers that evolve with the network.</p>
          </article>
          <article class="builder-card reveal">
            <div class="feature-icon">◈</div>
            <h3>Builder surface area</h3>
            <p>Node software, future SDK paths, and protocol interfaces that make the project feel open for builders early.</p>
          </article>
        </div>
      </div>
    </section>

    <section class="section" id="network">
      <div class="container">
        <div class="section-head reveal">
          <div>
            <h2>Network status</h2>
          </div>
          <p>
            Even placeholder live-style metrics make a project feel more real. Later, these can connect to your actual node data.
          </p>
        </div>

        <div class="network-layout">
          <div class="network-panel reveal">
            <span class="eyebrow-alt">Live panel</span>
            <h3>Netlithic testnet preview</h3>
            <div class="status-grid">
              <div class="network-row">
                <strong>Chain</strong>
                <span>Netlithic Testnet</span>
              </div>
              <div class="network-row">
                <strong>Consensus</strong>
                <span>Active</span>
              </div>
              <div class="network-row">
                <strong>Latest block</strong>
                <span>#1043</span>
              </div>
              <div class="network-row">
                <strong>Nodes</strong>
                <span>03 online</span>
              </div>
            </div>
            <div class="status-badges">
              <div class="status-badge">Open Source</div>
              <div class="status-badge">Community Governed</div>
              <div class="status-badge">Built in Public</div>
            </div>
          </div>

          <div class="protocol-card reveal">
            <span class="eyebrow-alt">Builders</span>
            <h3>Build on Netlithic</h3>
            <div class="status-list">
              <div class="mini-panel">
                <strong>Node software</strong>
                <p>Run the chain locally, test behavior, and participate in early network experimentation.</p>
              </div>
              <div class="mini-panel">
                <strong>Protocol tooling</strong>
                <p>Future-facing SDK and governance components give builders a reason to start early.</p>
              </div>
              <div class="mini-panel">
                <strong>AI-native future</strong>
                <p>Designed for a world where agents, automation, and coordination systems need reliable infrastructure.</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section class="section" id="community">
      <div class="container">
        <div class="section-head reveal">
          <div>
            <h2>Community momentum</h2>
          </div>
          <p>
            Big projects feel alive. Even before launch, your website should signal momentum across the places people gather.
          </p>
        </div>

        <div class="community-grid">
          <article class="community-card reveal">
            <span class="community-number">01</span>
            <h3>GitHub</h3>
            <p>Show active building, protocol progress, and a clear place for technical credibility to live.</p>
          </article>
          <article class="community-card reveal">
            <span class="community-number">02</span>
            <h3>Discord</h3>
            <p>Create gravity around announcements, governance discussion, builder feedback, and early believers.</p>
          </article>
          <article class="community-card reveal">
            <span class="community-number">03</span>
            <h3>X</h3>
            <p>Turn the public narrative into momentum with progress updates, mission posts, and launch signal boosts.</p>
          </article>
        </div>
      </div>
    </section>

    <section class="cta" id="cta">
      <div class="container">
        <div class="cta-box reveal">
          <img src="assets/netlithic-logo.png" alt="Netlithic wordmark" style="width:min(100%,340px);height:auto;display:block;margin-bottom:18px;object-fit:contain;" />
          <h2>Build in public. Launch with intention.</h2>
          <p>
            Netlithic does not need to look like every other crypto landing page. It should feel clean, premium, and serious enough
            that people immediately understand this is bigger than a meme coin splash screen.
          </p>
          <div class="hero-actions">
            <a class="btn btn-primary" href="https://github.com/IronNode951/Netlithic" target="_blank" rel="noreferrer">Open GitHub</a>
            <a class="btn btn-secondary" href="https://discord.gg/a92xq4du" target="_blank" rel="noreferrer">Join Discord</a>
            <a class="btn btn-secondary" href="https://x.com/netlithicchain" target="_blank" rel="noreferrer">Follow on X</a>
          </div>
        </div>
      </div>
    </section>
  </main>

  <footer class="footer">
    <div class="container footer-inner">
      <div>© 2026 Netlithic. Community-built blockchain vision.</div>
      <div>Docs · Whitepaper · GitHub · Discord · X · founder@netlithicchain.com</div>
    </div>
  </footer>

  <script>
    const observer = new IntersectionObserver((entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add('visible');
        }
      });
    }, { threshold: 0.14 });

    document.querySelectorAll('.reveal').forEach((el, index) => {
      if (!el.classList.contains('visible')) {
        el.style.transitionDelay = `${Math.min(index * 70, 280)}ms`;
      }
      observer.observe(el);
    });
  </script>
</body>
</html>

