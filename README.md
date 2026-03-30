<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Nevara · AI Call Auditing · Case Study</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=DM+Mono:wght@400;500&family=Fraunces:ital,opsz,wght@0,9..144,300;0,9..144,400;1,9..144,300&family=Inter:wght@400;500;600&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --ink: #0f0f0e;
    --ink2: #3a3a38;
    --ink3: #6b6b67;
    --line: #e3e2dd;
    --line2: #c8c7c1;
    --bg: #f7f6f2;
    --bg2: #ffffff;
    --accent: #1a4a3a;
    --accent2: #2d7a5f;
    --accent3: #e8f5f0;
    --amber: #92580a;
    --amber-bg: #fdf3e3;
    --blue: #1a3a5c;
    --blue-bg: #e8f0f8;
    --coral: #8c2f1f;
    --coral-bg: #fdf0ed;
    --mono: 'DM Mono', monospace;
    --serif: 'Fraunces', serif;
    --sans: 'Inter', -apple-system, sans-serif;
  }

  html { scroll-behavior: smooth; }

  body {
    font-family: var(--sans);
    background: var(--bg);
    color: var(--ink);
    line-height: 1.65;
    font-size: 15px;
  }

  /* ── NAV ── */
  nav {
    position: sticky; top: 0; z-index: 100;
    background: rgba(247,246,242,0.92);
    backdrop-filter: blur(12px);
    border-bottom: 1px solid var(--line);
    padding: 0 2rem;
    display: flex; align-items: center; justify-content: space-between;
    height: 56px;
  }
  .nav-logo {
    font-family: var(--mono);
    font-size: 13px;
    font-weight: 500;
    color: var(--ink2);
    text-decoration: none;
    display: flex; align-items: center; gap: 8px;
  }
  .nav-logo .dot {
    width: 8px; height: 8px;
    background: var(--accent2);
    border-radius: 50%;
  }
  .nav-links {
    display: flex; gap: 1.5rem;
    list-style: none;
  }
  .nav-links a {
    font-size: 12px; color: var(--ink3);
    text-decoration: none; letter-spacing: 0.04em;
    text-transform: uppercase; font-weight: 500;
    transition: color 0.2s;
  }
  .nav-links a:hover { color: var(--ink); }

  /* ── HERO ── */
  .hero {
    padding: 5rem 2rem 4rem;
    max-width: 780px;
    margin: 0 auto;
    border-bottom: 1px solid var(--line);
  }
  .hero-tag {
    display: inline-flex; align-items: center; gap: 6px;
    background: var(--accent3);
    color: var(--accent);
    font-size: 11px; font-weight: 600;
    letter-spacing: 0.08em; text-transform: uppercase;
    padding: 4px 10px;
    border-radius: 4px;
    margin-bottom: 1.5rem;
  }
  .hero h1 {
    font-family: var(--serif);
    font-size: clamp(2.4rem, 5vw, 3.6rem);
    font-weight: 300;
    line-height: 1.15;
    letter-spacing: -0.02em;
    color: var(--ink);
    margin-bottom: 1.25rem;
  }
  .hero h1 em { font-style: italic; color: var(--accent2); }
  .hero-sub {
    font-size: 1.05rem;
    color: var(--ink2);
    max-width: 560px;
    line-height: 1.7;
    margin-bottom: 2rem;
  }
  .meta-row {
    display: flex; flex-wrap: wrap; gap: 1rem;
  }
  .meta-pill {
    display: flex; align-items: center; gap: 6px;
    border: 1px solid var(--line2);
    border-radius: 6px;
    padding: 6px 12px;
    font-size: 12px;
    color: var(--ink2);
    background: var(--bg2);
  }
  .meta-pill span { color: var(--ink3); }

  /* ── LAYOUT ── */
  .wrapper {
    max-width: 1100px;
    margin: 0 auto;
    padding: 0 2rem;
    display: grid;
    grid-template-columns: 200px 1fr;
    gap: 0;
  }

  /* ── SIDEBAR ── */
  .sidebar {
    padding: 3rem 2rem 3rem 0;
    border-right: 1px solid var(--line);
    position: sticky;
    top: 56px;
    align-self: start;
    height: calc(100vh - 56px);
    overflow-y: auto;
  }
  .sidebar-label {
    font-size: 10px; font-weight: 600;
    letter-spacing: 0.1em; text-transform: uppercase;
    color: var(--ink3);
    margin-bottom: 0.75rem;
    margin-top: 1.5rem;
  }
  .sidebar-label:first-child { margin-top: 0; }
  .sidebar nav a {
    display: block;
    font-size: 12.5px;
    color: var(--ink3);
    text-decoration: none;
    padding: 4px 0;
    border-left: 2px solid transparent;
    padding-left: 10px;
    margin-left: -10px;
    transition: all 0.15s;
  }
  .sidebar nav a:hover, .sidebar nav a.active {
    color: var(--accent);
    border-left-color: var(--accent2);
  }

  /* ── CONTENT ── */
  .content {
    padding: 3rem 0 3rem 3rem;
  }

  section { margin-bottom: 4rem; }
  section:last-child { margin-bottom: 0; }

  h2 {
    font-family: var(--serif);
    font-size: 1.85rem;
    font-weight: 300;
    letter-spacing: -0.02em;
    color: var(--ink);
    margin-bottom: 1.25rem;
    padding-bottom: 0.75rem;
    border-bottom: 1px solid var(--line);
  }
  h3 {
    font-size: 0.8rem; font-weight: 600;
    letter-spacing: 0.08em; text-transform: uppercase;
    color: var(--ink3);
    margin-bottom: 0.75rem;
    margin-top: 2rem;
  }
  h3:first-child { margin-top: 0; }
  p { color: var(--ink2); margin-bottom: 1rem; }
  p:last-child { margin-bottom: 0; }

  /* ── STAT GRID ── */
  .stat-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
    gap: 12px;
    margin: 1.5rem 0;
  }
  .stat-card {
    background: var(--bg2);
    border: 1px solid var(--line);
    border-radius: 10px;
    padding: 1rem 1.1rem;
  }
  .stat-card .num {
    font-family: var(--mono);
    font-size: 1.6rem;
    font-weight: 500;
    color: var(--ink);
    display: block;
    line-height: 1;
    margin-bottom: 4px;
  }
  .stat-card .lbl {
    font-size: 11px; color: var(--ink3);
    text-transform: uppercase; letter-spacing: 0.06em;
  }

  /* ── PIPELINE DIAGRAM ── */
  .pipeline {
    margin: 1.5rem 0;
    display: flex;
    flex-direction: column;
    gap: 3px;
  }
  .pipe-row {
    display: flex;
    align-items: stretch;
    gap: 3px;
  }
  .pipe-node {
    flex: 1;
    background: var(--bg2);
    border: 1px solid var(--line);
    border-radius: 8px;
    padding: 0.9rem 1rem;
    position: relative;
  }
  .pipe-node.active {
    border-color: var(--accent2);
    background: var(--accent3);
  }
  .pipe-node .pn-label {
    font-size: 11px; font-weight: 600;
    letter-spacing: 0.06em; text-transform: uppercase;
    color: var(--ink3);
    margin-bottom: 3px;
  }
  .pipe-node.active .pn-label { color: var(--accent); }
  .pipe-node .pn-title {
    font-size: 13px; font-weight: 500;
    color: var(--ink);
    margin-bottom: 2px;
  }
  .pipe-node .pn-sub {
    font-size: 11.5px;
    color: var(--ink3);
    line-height: 1.5;
  }
  .pipe-arrow {
    display: flex; align-items: center; justify-content: center;
    color: var(--ink3); font-size: 14px;
    padding: 0 2px;
    flex-shrink: 0;
  }

  /* ── STACK CHIPS ── */
  .chip-group {
    display: flex; flex-wrap: wrap; gap: 6px;
    margin: 1rem 0;
  }
  .chip {
    font-family: var(--mono);
    font-size: 11px; font-weight: 500;
    padding: 4px 9px;
    border-radius: 4px;
    border: 1px solid var(--line2);
    color: var(--ink2);
    background: var(--bg2);
    white-space: nowrap;
  }
  .chip.green  { background: var(--accent3);  border-color: #a3d4c2; color: var(--accent); }
  .chip.amber  { background: var(--amber-bg); border-color: #f0d4a0; color: var(--amber); }
  .chip.blue   { background: var(--blue-bg);  border-color: #afc8e4; color: var(--blue); }
  .chip.coral  { background: var(--coral-bg); border-color: #e8bdb4; color: var(--coral); }

  /* ── CALLOUT ── */
  .callout {
    border-left: 3px solid var(--accent2);
    background: var(--accent3);
    border-radius: 0 8px 8px 0;
    padding: 1rem 1.25rem;
    margin: 1.5rem 0;
  }
  .callout p { color: var(--accent); margin: 0; font-size: 14px; line-height: 1.6; }
  .callout strong { font-weight: 600; }
  .callout.amber {
    border-left-color: #d4900a;
    background: var(--amber-bg);
  }
  .callout.amber p { color: var(--amber); }
  .callout.blue {
    border-left-color: #2a6aad;
    background: var(--blue-bg);
  }
  .callout.blue p { color: var(--blue); }

  /* ── CODE ── */
  .code-block {
    background: #1a1a18;
    border-radius: 8px;
    padding: 1.1rem 1.25rem;
    margin: 1rem 0;
    overflow-x: auto;
  }
  .code-block pre {
    font-family: var(--mono);
    font-size: 12px;
    color: #c8c7bf;
    line-height: 1.7;
    white-space: pre;
  }
  .code-block .tok-key  { color: #7dd3b6; }
  .code-block .tok-str  { color: #f5a97f; }
  .code-block .tok-num  { color: #a8d9ff; }
  .code-block .tok-cmt  { color: #6b6b67; }
  .code-block .tok-fn   { color: #c3a6ff; }

  /* ── MICROSERVICE CARDS ── */
  .ms-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 12px;
    margin: 1.5rem 0;
  }
  .ms-card {
    background: var(--bg2);
    border: 1px solid var(--line);
    border-radius: 10px;
    padding: 1.1rem 1.2rem;
  }
  .ms-card .ms-icon {
    width: 32px; height: 32px;
    border-radius: 8px;
    display: flex; align-items: center; justify-content: center;
    font-size: 15px;
    margin-bottom: 0.75rem;
  }
  .ms-card .ms-name {
    font-size: 13px; font-weight: 600;
    color: var(--ink);
    margin-bottom: 4px;
  }
  .ms-card .ms-desc {
    font-size: 12px; color: var(--ink3);
    line-height: 1.55;
    margin-bottom: 0.75rem;
  }
  .ms-card .ms-tags {
    display: flex; flex-wrap: wrap; gap: 4px;
  }
  .ms-tag {
    font-family: var(--mono);
    font-size: 10px;
    padding: 2px 6px;
    border-radius: 3px;
    border: 1px solid var(--line2);
    color: var(--ink3);
  }
  .ms-card.tc { border-top: 3px solid var(--accent2); }
  .ms-card.ta { border-top: 3px solid #d4900a; }
  .ms-card.tb { border-top: 3px solid #2a6aad; }
  .ms-card.tp { border-top: 3px solid #c2446e; }

  /* ── FLOW DIAGRAM ── */
  .flow-diagram {
    background: var(--bg2);
    border: 1px solid var(--line);
    border-radius: 10px;
    padding: 1.5rem;
    margin: 1.5rem 0;
    overflow-x: auto;
  }
  .flow-diagram svg { display: block; min-width: 560px; }

  /* ── TRADEOFFS TABLE ── */
  .tradeoff-table {
    width: 100%;
    border-collapse: collapse;
    margin: 1.5rem 0;
    font-size: 13px;
  }
  .tradeoff-table th {
    text-align: left;
    padding: 8px 12px;
    font-size: 10px;
    font-weight: 600;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    color: var(--ink3);
    background: var(--bg);
    border-bottom: 1px solid var(--line);
  }
  .tradeoff-table td {
    padding: 10px 12px;
    border-bottom: 1px solid var(--line);
    color: var(--ink2);
    vertical-align: top;
  }
  .tradeoff-table tr:last-child td { border-bottom: none; }
  .tradeoff-table td:first-child {
    font-family: var(--mono);
    font-size: 12px;
    font-weight: 500;
    color: var(--ink);
    white-space: nowrap;
  }
  .good { color: #2d7a5f; font-size: 12px; }
  .bad  { color: #a32d2d; font-size: 12px; }

  /* ── CHALLENGE CARDS ── */
  .challenge-list {
    display: flex; flex-direction: column; gap: 10px;
    margin: 1.5rem 0;
  }
  .challenge {
    background: var(--bg2);
    border: 1px solid var(--line);
    border-radius: 8px;
    padding: 1rem 1.1rem;
    display: grid;
    grid-template-columns: auto 1fr;
    gap: 1rem;
    align-items: start;
  }
  .challenge-num {
    font-family: var(--mono);
    font-size: 12px; font-weight: 500;
    color: var(--accent2);
    padding: 3px 7px;
    background: var(--accent3);
    border-radius: 4px;
    white-space: nowrap;
  }
  .challenge-title {
    font-size: 13px; font-weight: 600;
    color: var(--ink);
    margin-bottom: 4px;
  }
  .challenge-body { font-size: 12.5px; color: var(--ink3); line-height: 1.6; }

  /* ── FOOTER ── */
  footer {
    border-top: 1px solid var(--line);
    padding: 2rem;
    text-align: center;
    font-size: 12px;
    color: var(--ink3);
    background: var(--bg);
  }
  footer a { color: var(--accent2); text-decoration: none; }

  @media (max-width: 768px) {
    .wrapper { grid-template-columns: 1fr; }
    .sidebar { display: none; }
    .content { padding: 2rem 0; }
    .ms-grid { grid-template-columns: 1fr; }
  }
</style>
</head>
<body>

<!-- NAV -->
<nav>
  <a class="nav-logo" href="#">
    <span class="dot"></span>
    nevara · case study
  </a>
  <ul class="nav-links">
    <li><a href="#problem">Problem</a></li>
    <li><a href="#architecture">Architecture</a></li>
    <li><a href="#pipeline">Pipeline</a></li>
    <li><a href="#challenges">Challenges</a></li>
    <li><a href="#stack">Stack</a></li>
  </ul>
</nav>

<!-- HERO -->
<header class="hero">
  <div class="hero-tag">AI Engineering · Production System · NLP</div>
  <h1>Cloning a sales coach's brain<br>with <em>production GenAI</em></h1>
  <p class="hero-sub">
    Built a full-stack AI call auditing platform at Blue AI Labs that replicated the coaching style
    of an elite sales coach — producing structured, actionable call audit reports at scale from
    real sales call transcripts via Gong and Fathom integrations.
  </p>
  <div class="meta-row">
    <div class="meta-pill">
      <svg width="12" height="12" viewBox="0 0 16 16" fill="none"><circle cx="8" cy="8" r="7" stroke="currentColor" stroke-width="1.5"/><path d="M8 4v4l3 2" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/></svg>
      <span>Role:</span> AI/ML Engineer Intern
    </div>
    <div class="meta-pill">
      <svg width="12" height="12" viewBox="0 0 16 16" fill="none"><rect x="2" y="3" width="12" height="11" rx="2" stroke="currentColor" stroke-width="1.5"/><path d="M5 1v4M11 1v4M2 8h12" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/></svg>
      <span>Company:</span> Blue AI Labs
    </div>
    <div class="meta-pill">
      <svg width="12" height="12" viewBox="0 0 16 16" fill="none"><path d="M8 2L10 6h4l-3.5 2.5 1.5 4L8 10l-4 2.5L5.5 8.5 2 6h4z" stroke="currentColor" stroke-width="1.5" stroke-linejoin="round"/></svg>
      <span>Domain:</span> Sales Coaching AI, LLM Systems
    </div>
    <div class="meta-pill">
      <svg width="12" height="12" viewBox="0 0 16 16" fill="none"><path d="M2 14l4-4m0 0l5-5m-5 5l-1-3 7-7 3 3-7 7-3-1z" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/></svg>
      <span>System:</span> Production · Deployed to Vercel + AWS Lambda
    </div>
  </div>
</header>

<!-- MAIN BODY -->
<div class="wrapper">

  <!-- SIDEBAR -->
  <aside class="sidebar">
    <p class="sidebar-label">Sections</p>
    <nav>
      <a href="#problem">Problem Statement</a>
      <a href="#impact">Business Impact</a>
      <a href="#architecture">System Architecture</a>
      <a href="#pipeline">AI Pipeline</a>
      <a href="#microservices">Microservices</a>
      <a href="#feedback">Feedback Loop</a>
      <a href="#challenges">Engineering Challenges</a>
      <a href="#stack">Tech Stack</a>
      <a href="#learnings">Key Learnings</a>
    </nav>
    <p class="sidebar-label" style="margin-top:2rem">Models Used</p>
    <nav>
      <a href="#pipeline">GPT-4.1 (Notes)</a>
      <a href="#pipeline">GPT-4o (Reports)</a>
      <a href="#pipeline">Deepgram nova-3</a>
    </nav>
    <p class="sidebar-label" style="margin-top:2rem">Infra</p>
    <nav>
      <a href="#stack">AWS Lambda</a>
      <a href="#stack">Supabase + Prisma</a>
      <a href="#stack">Vercel CI/CD</a>
    </nav>
  </aside>

  <!-- CONTENT -->
  <main class="content">

    <!-- PROBLEM -->
    <section id="problem">
      <h2>The problem</h2>
      <p>
        Elite sales coaches like Mor Assouline spend hours manually reviewing call recordings and
        producing bespoke audit reports — detailed documents that highlight a rep's strengths,
        areas of improvement, and specific tactical fixes with exact timestamps.
      </p>
      <p>
        The challenge: this coaching style is deeply personal. It has a specific tone, a structured
        format, and actionable specificity that's hard to generalize. The goal was not to build
        "a generic AI feedback tool" — it was to <strong>digitize one coach's expertise</strong>
        and scale it to every rep, every call, automatically.
      </p>
      <div class="callout">
        <p>
          <strong>Core problem:</strong> Can we make GPT-4 produce audit reports that are
          indistinguishable in style, structure, and insight quality from those hand-written by
          an expert human coach?
        </p>
      </div>
      <p>
        The system needed to ingest calls from Gong and Fathom (the dominant sales call tools),
        generate per-call coaching notes, aggregate them into consolidated representative reports,
        and continuously improve based on coach feedback.
      </p>
    </section>

    <!-- IMPACT -->
    <section id="impact">
      <h2>Business impact</h2>
      <div class="stat-grid">
        <div class="stat-card">
          <span class="num">~10×</span>
          <span class="lbl">Coaching throughput</span>
        </div>
        <div class="stat-card">
          <span class="num">&lt;2min</span>
          <span class="lbl">Time to full report</span>
        </div>
        <div class="stat-card">
          <span class="num">99.9%</span>
          <span class="lbl">Lambda availability</span>
        </div>
        <div class="stat-card">
          <span class="num">4-stage</span>
          <span class="lbl">AI microservice pipeline</span>
        </div>
        <div class="stat-card">
          <span class="num">Gong + Fathom</span>
          <span class="lbl">Integrations</span>
        </div>
        <div class="stat-card">
          <span class="num">Notion</span>
          <span class="lbl">Export destination</span>
        </div>
      </div>
      <p>
        A sales coach who previously spent 45–90 minutes per call audit can now review and
        approve an AI-generated report in under 5 minutes. The system also enables multi-call
        "representative reports" that surface cross-call patterns — something that was
        previously impossible to do manually at scale.
      </p>
    </section>

    <!-- ARCHITECTURE -->
    <section id="architecture">
      <h2>System architecture</h2>
      <p>
        The platform is built as a Next.js frontend calling a set of independent FastAPI
        microservices — each deployed as an AWS Lambda function. Supabase (Postgres) handles
        persistence, authentication, and file storage.
      </p>

      <div class="flow-diagram">
        <svg width="100%" viewBox="0 0 620 360" xmlns="http://www.w3.org/2000/svg" style="font-family:'Inter',sans-serif">
          <defs>
            <marker id="arr" viewBox="0 0 10 10" refX="8" refY="5" markerWidth="5" markerHeight="5" orient="auto-start-reverse">
              <path d="M2 1L8 5L2 9" fill="none" stroke="#6b6b67" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
            </marker>
          </defs>

          <!-- Frontend -->
          <rect x="10" y="140" width="100" height="80" rx="8" fill="#e8f5f0" stroke="#a3d4c2" stroke-width="1"/>
          <text x="60" y="175" text-anchor="middle" font-size="12" font-weight="600" fill="#1a4a3a">Next.js</text>
          <text x="60" y="191" text-anchor="middle" font-size="10" fill="#2d7a5f">Frontend + API Routes</text>
          <text x="60" y="207" text-anchor="middle" font-size="10" fill="#2d7a5f">Vercel / SSE streaming</text>

          <!-- Arrow FE → Lambda group -->
          <line x1="110" y1="180" x2="148" y2="180" stroke="#6b6b67" stroke-width="1" marker-end="url(#arr)"/>

          <!-- Lambda group container -->
          <rect x="150" y="60" width="260" height="240" rx="10" fill="none" stroke="#c8c7c1" stroke-width="1" stroke-dasharray="5 4"/>
          <text x="280" y="82" text-anchor="middle" font-size="10" fill="#6b6b67" letter-spacing="0.08em">AWS LAMBDA FUNCTIONS</text>

          <!-- Transcription -->
          <rect x="165" y="92" width="105" height="52" rx="6" fill="#fdf3e3" stroke="#f0d4a0" stroke-width="1"/>
          <text x="217" y="114" text-anchor="middle" font-size="11" font-weight="600" fill="#92580a">Transcription</text>
          <text x="217" y="130" text-anchor="middle" font-size="10" fill="#92580a">Deepgram nova-3</text>

          <!-- Call Notes -->
          <rect x="290" y="92" width="105" height="52" rx="6" fill="#e8f0f8" stroke="#afc8e4" stroke-width="1"/>
          <text x="342" y="114" text-anchor="middle" font-size="11" font-weight="600" fill="#1a3a5c">Call Notes</text>
          <text x="342" y="130" text-anchor="middle" font-size="10" fill="#1a3a5c">GPT-4.1</text>

          <!-- Arrow T → CN -->
          <line x1="270" y1="118" x2="288" y2="118" stroke="#6b6b67" stroke-width="1" marker-end="url(#arr)"/>

          <!-- AI Report -->
          <rect x="165" y="168" width="105" height="52" rx="6" fill="#fdf0ed" stroke="#e8bdb4" stroke-width="1"/>
          <text x="217" y="190" text-anchor="middle" font-size="11" font-weight="600" fill="#8c2f1f">AI Report</text>
          <text x="217" y="206" text-anchor="middle" font-size="10" fill="#8c2f1f">GPT-4o</text>

          <!-- Feedback Retrain -->
          <rect x="290" y="168" width="105" height="52" rx="6" fill="#e8f5f0" stroke="#a3d4c2" stroke-width="1"/>
          <text x="342" y="190" text-anchor="middle" font-size="11" font-weight="600" fill="#1a4a3a">Feedback</text>
          <text x="342" y="206" text-anchor="middle" font-size="10" fill="#1a4a3a">Retrain loop</text>

          <!-- Arrows between lambdas -->
          <line x1="217" y1="144" x2="217" y2="166" stroke="#6b6b67" stroke-width="1" marker-end="url(#arr)"/>
          <line x1="342" y1="144" x2="342" y2="166" stroke="#6b6b67" stroke-width="1" marker-end="url(#arr)"/>
          <line x1="270" y1="194" x2="288" y2="194" stroke="#6b6b67" stroke-width="1" marker-end="url(#arr)"/>

          <!-- Knowledge Base -->
          <rect x="165" y="248" width="230" height="40" rx="6" fill="#f7f6f2" stroke="#c8c7c1" stroke-width="1"/>
          <text x="280" y="272" text-anchor="middle" font-size="11" font-weight="600" fill="#3a3a38">Knowledge Base (XML)</text>

          <!-- Arrow Feedback → KB -->
          <line x1="342" y1="220" x2="342" y2="248" stroke="#6b6b67" stroke-width="0.8" stroke-dasharray="3 3" marker-end="url(#arr)"/>
          <line x1="217" y1="220" x2="217" y2="248" stroke="#6b6b67" stroke-width="0.8" stroke-dasharray="3 3" marker-end="url(#arr)"/>

          <!-- Arrow Lambda → Supabase -->
          <line x1="412" y1="180" x2="448" y2="180" stroke="#6b6b67" stroke-width="1" marker-end="url(#arr)"/>

          <!-- Supabase -->
          <rect x="450" y="120" width="110" height="120" rx="8" fill="#f7f6f2" stroke="#c8c7c1" stroke-width="1"/>
          <text x="505" y="153" text-anchor="middle" font-size="12" font-weight="600" fill="#3a3a38">Supabase</text>
          <text x="505" y="170" text-anchor="middle" font-size="10" fill="#6b6b67">Postgres + Prisma</text>
          <text x="505" y="186" text-anchor="middle" font-size="10" fill="#6b6b67">OAuth (Auth)</text>
          <text x="505" y="202" text-anchor="middle" font-size="10" fill="#6b6b67">File Storage</text>
          <text x="505" y="218" text-anchor="middle" font-size="10" fill="#6b6b67">Transcripts / Reports</text>

          <!-- Gong/Fathom top -->
          <rect x="10" y="30" width="100" height="50" rx="6" fill="#f7f6f2" stroke="#c8c7c1" stroke-width="1"/>
          <text x="60" y="52" text-anchor="middle" font-size="11" font-weight="600" fill="#3a3a38">Gong</text>
          <text x="60" y="68" text-anchor="middle" font-size="10" fill="#6b6b67">Call recordings</text>

          <rect x="10" y="90" width="100" height="50" rx="6" fill="#f7f6f2" stroke="#c8c7c1" stroke-width="1"/>
          <text x="60" y="112" text-anchor="middle" font-size="11" font-weight="600" fill="#3a3a38">Fathom</text>
          <text x="60" y="128" text-anchor="middle" font-size="10" fill="#6b6b67">+ HLS proxy</text>

          <!-- Arrows Gong/Fathom → FE -->
          <line x1="110" y1="55" x2="130" y2="140" stroke="#6b6b67" stroke-width="0.8" stroke-dasharray="3 3" marker-end="url(#arr)"/>
          <line x1="110" y1="115" x2="120" y2="140" stroke="#6b6b67" stroke-width="0.8" stroke-dasharray="3 3" marker-end="url(#arr)"/>

          <!-- Notion export -->
          <rect x="450" y="270" width="110" height="40" rx="6" fill="#f7f6f2" stroke="#c8c7c1" stroke-width="1"/>
          <text x="505" y="295" text-anchor="middle" font-size="11" fill="#3a3a38">Notion export</text>
          <line x1="505" y1="240" x2="505" y2="268" stroke="#6b6b67" stroke-width="0.8" stroke-dasharray="3 3" marker-end="url(#arr)"/>

          <!-- Legend -->
          <line x1="10" y1="330" x2="30" y2="330" stroke="#6b6b67" stroke-width="1" marker-end="url(#arr)"/>
          <text x="36" y="334" font-size="9" fill="#6b6b67">Data flow</text>
          <line x1="90" y1="330" x2="110" y2="330" stroke="#6b6b67" stroke-width="0.8" stroke-dasharray="3 3" marker-end="url(#arr)"/>
          <text x="116" y="334" font-size="9" fill="#6b6b67">Trigger / async</text>
        </svg>
      </div>

      <h3>Data ingestion</h3>
      <p>
        Calls enter the system in two ways: direct audio/video upload (transcribed via Deepgram),
        or via a Gong or Fathom share link. A Puppeteer-based headless browser scrapes the media
        URL; a custom HLS proxy (via <code>/api/hls/m3u8</code> and <code>/api/hls/seg</code>)
        handles CORS restrictions on Fathom's HLS streams. Transcripts are always user-pasted
        (never scraped) for downstream AI reliability.
      </p>
    </section>

    <!-- PIPELINE -->
    <section id="pipeline">
      <h2>AI pipeline</h2>
      <p>
        The system follows a two-stage AI pipeline: per-call note generation, followed by
        multi-call report aggregation. Both stages use versioned prompt systems and a curated
        Knowledge Base (XML) that encodes the coach's style preferences.
      </p>

      <div class="pipeline">
        <div class="pipe-row">
          <div class="pipe-node active">
            <div class="pn-label">Stage 1</div>
            <div class="pn-title">Call Notes Generation</div>
            <div class="pn-sub">GPT-4.1 · FastAPI on AWS Lambda · 15–30s per call</div>
          </div>
          <div class="pipe-arrow">→</div>
          <div class="pipe-node active">
            <div class="pn-label">Stage 2</div>
            <div class="pn-title">Representative Report</div>
            <div class="pn-sub">GPT-4o · Multi-call context fusion · 60–120s</div>
          </div>
        </div>
        <div style="text-align:center; font-size: 11px; color: var(--ink3); padding: 4px 0;">↑ outputs feed into ↓</div>
        <div class="pipe-row">
          <div class="pipe-node">
            <div class="pn-label">Input</div>
            <div class="pn-title">Transcript + Guidelines</div>
            <div class="pn-sub">Speaker-diarized, timestamped</div>
          </div>
          <div class="pipe-arrow">→</div>
          <div class="pipe-node">
            <div class="pn-label">Knowledge Base</div>
            <div class="pn-title">Coach's Style XML</div>
            <div class="pn-sub">Tone, banned phrases, examples</div>
          </div>
          <div class="pipe-arrow">→</div>
          <div class="pipe-node">
            <div class="pn-label">Output</div>
            <div class="pn-title">Structured XML Report</div>
            <div class="pn-sub">Priority fixes, action items, analytics</div>
          </div>
        </div>
      </div>

      <h3>Prompt engineering architecture</h3>
      <p>
        Prompts are modular and versioned. The <code>v2</code> system uses coaching questions
        as the primary scaffold — forcing GPT to evaluate each call moment against specific
        sales methodology criteria (discovery, demo, next steps, showmanship).
      </p>

      <div class="code-block">
        <pre>
<span class="tok-cmt"># prompt_v2/ directory structure</span>
<span class="tok-fn">01_persona.md</span>      <span class="tok-cmt"># "You are Mor Assouline, elite B2B sales coach..."</span>
<span class="tok-fn">02_task.md</span>         <span class="tok-cmt"># Task specification with coaching methodology</span>
<span class="tok-fn">03_output_format.md</span> <span class="tok-cmt"># XML schema: Fix, Priority, AOI, Pros, FixExample</span>
<span class="tok-fn">04_examples.md</span>     <span class="tok-cmt"># 3 real transcript → note pairs (few-shot)</span>
<span class="tok-fn">05_graph_analysis.md</span> <span class="tok-cmt"># Graph data extraction for analytics charts</span>
<span class="tok-fn">guidelines/</span>        <span class="tok-cmt"># Domain-specific coaching rules (appended if enabled)</span>

<span class="tok-cmt"># Output format (delimiter-based for robustness)</span>
<span class="tok-str">02:15 ||| Rep: "What are your main priorities?" ||| </span>
<span class="tok-str">Strong discovery question to identify pain points. ||| Discovery,Pros</span>
<span class="tok-str">---NOTES_SEPARATOR---</span>
<span class="tok-str">05:30 ||| Rep: "Let me show you how this works..." ||| </span>
<span class="tok-str">Jumped into demo without sufficient discovery. ||| Demo,AOI</span>
        </pre>
      </div>

      <h3>Context building strategy</h3>
      <p>
        The report service uses a hybrid context strategy: <code>TRANSCRIPT_WEIGHT = 0.0</code>
        (notes-focused, not raw transcript) with a 50,000 character context budget. For
        multi-call representative reports, the context builder enforces call ratio requirements
        (e.g., "pattern must appear in 3/5 calls") and prevents contradictions between Pros
        and Areas of Improvement.
      </p>

      <div class="callout amber">
        <p>
          <strong>Key insight:</strong> Prioritizing structured call notes over raw transcripts
          for report generation significantly improved coherence. The model reasoned over
          pre-filtered signal rather than noisy transcription artifacts.
        </p>
      </div>
    </section>

    <!-- MICROSERVICES -->
    <section id="microservices">
      <h2>Microservice breakdown</h2>
      <p>
        Four independent FastAPI services, each packaged as an AWS Lambda ZIP using Docker-based
        dependency compilation targeting the Amazon Linux runtime.
      </p>

      <div class="ms-grid">
        <div class="ms-card tc">
          <div class="ms-icon" style="background: var(--amber-bg)">🎙️</div>
          <div class="ms-name">Transcription Service</div>
          <div class="ms-desc">
            Converts audio/video to speaker-diarized, timestamped transcripts. Uses Deepgram
            nova-3 with diarization + punctuation. Outputs <code>[Speaker:N] [mm:ss] text</code>
            format. Falls back to word-level data if utterances are missing.
          </div>
          <div class="ms-tags">
            <span class="ms-tag">Deepgram nova-3</span>
            <span class="ms-tag">diarization</span>
            <span class="ms-tag">httpx async</span>
            <span class="ms-tag">180s timeout</span>
          </div>
        </div>

        <div class="ms-card ta">
          <div class="ms-icon" style="background: var(--blue-bg)">📝</div>
          <div class="ms-name">Call Notes Microservice</div>
          <div class="ms-desc">
            Converts a transcript + optional coaching guidelines into structured,
            timestamped coaching notes. Uses a versioned prompt system (v2 production).
            Bulk inserts notes to Supabase via Prisma. Streams progress via SSE.
          </div>
          <div class="ms-tags">
            <span class="ms-tag">GPT-4.1</span>
            <span class="ms-tag">SSE streaming</span>
            <span class="ms-tag">$0.10–0.50/call</span>
            <span class="ms-tag">15–30s</span>
          </div>
        </div>

        <div class="ms-card tb">
          <div class="ms-icon" style="background: var(--coral-bg)">📊</div>
          <div class="ms-name">AI Report Service</div>
          <div class="ms-desc">
            Two-stage generation: (1) full XML audit report, (2) separate AI call extracts
            graph data (pie + bar charts). Supports single-call and multi-call representative
            analysis. Embeds <code>CallAnalytics</code> section into the XML.
          </div>
          <div class="ms-tags">
            <span class="ms-tag">GPT-4o</span>
            <span class="ms-tag">XML output</span>
            <span class="ms-tag">Chart.js graphs</span>
            <span class="ms-tag">Notion export</span>
          </div>
        </div>

        <div class="ms-card tp">
          <div class="ms-icon" style="background: var(--accent3)">🔄</div>
          <div class="ms-name">Feedback Retrain</div>
          <div class="ms-desc">
            Closes the loop: user thumbs up/down ratings (1–5) trigger a Knowledge Base
            update. GPT-4.1 analyzes rated notes and rewrites the XML style guide.
            Versioned backups ensure rollback capability.
          </div>
          <div class="ms-tags">
            <span class="ms-tag">GPT-4.1</span>
            <span class="ms-tag">XML KB update</span>
            <span class="ms-tag">compression mode</span>
            <span class="ms-tag">$0.05–0.15</span>
          </div>
        </div>
      </div>

      <h3>Lambda configuration</h3>
      <table class="tradeoff-table">
        <thead>
          <tr>
            <th>Service</th>
            <th>Memory</th>
            <th>Timeout</th>
            <th>Concurrency</th>
            <th>Latency</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>Transcription</td>
            <td>512–1024 MB</td>
            <td>120–180s</td>
            <td>Reserved: 20</td>
            <td>Scales with audio length</td>
          </tr>
          <tr>
            <td>Call Notes</td>
            <td>512 MB</td>
            <td>120s</td>
            <td>Reserved: 20, Provisioned: 5</td>
            <td>15–30s</td>
          </tr>
          <tr>
            <td>AI Report</td>
            <td>1024–2048 MB</td>
            <td>240s</td>
            <td>Reserved: 20, Provisioned: 5</td>
            <td>60–120s (rep: 2–4min)</td>
          </tr>
          <tr>
            <td>Feedback Retrain</td>
            <td>512 MB</td>
            <td>120s</td>
            <td>Reserved: 10</td>
            <td>15–30s</td>
          </tr>
        </tbody>
      </table>
    </section>

    <!-- FEEDBACK LOOP -->
    <section id="feedback">
      <h2>Feedback & continuous improvement</h2>
      <p>
        The most novel part of the system is its self-improvement loop. Every AI-generated note
        carries a rating (thumbs up = +1, thumbs down = −1). When a call is marked as reviewed,
        the Feedback Retrain service analyzes the rated notes and updates the coach's Knowledge
        Base XML.
      </p>

      <div class="pipeline">
        <div class="pipe-row">
          <div class="pipe-node">
            <div class="pn-label">Step 1</div>
            <div class="pn-title">User rates notes</div>
            <div class="pn-sub">Rating: +1 (good) or −1 (bad)</div>
          </div>
          <div class="pipe-arrow">→</div>
          <div class="pipe-node">
            <div class="pn-label">Step 2</div>
            <div class="pn-title">Notes fetched by rating</div>
            <div class="pn-sub">Prisma query: Rating = ±1</div>
          </div>
          <div class="pipe-arrow">→</div>
          <div class="pipe-node active">
            <div class="pn-label">Step 3</div>
            <div class="pn-title">GPT rewrites KB</div>
            <div class="pn-sub">Adds/removes style rules</div>
          </div>
          <div class="pipe-arrow">→</div>
          <div class="pipe-node">
            <div class="pn-label">Step 4</div>
            <div class="pn-title">Versioned XML saved</div>
            <div class="pn-sub">Timestamped backup + rollback</div>
          </div>
        </div>
      </div>

      <div class="callout">
        <p>
          <strong>Design tradeoff:</strong> Two compression modes — ENABLED (deduplicate,
          merge, keep most actionable) and DISABLED (preserve breadth, only remove
          explicitly flagged items). Coaching style grows in specificity without
          the KB becoming unboundedly large.
        </p>
      </div>

      <h3>Knowledge base schema</h3>
      <div class="code-block">
        <pre>
<span class="tok-key">&lt;StyleGuide&gt;</span>
  <span class="tok-key">&lt;Tone&gt;</span>
    <span class="tok-str">&lt;Preferred&gt;</span>Professional, calm, precise, and human<span class="tok-str">&lt;/Preferred&gt;</span>
    <span class="tok-str">&lt;Avoid&gt;</span>Salesy, pushy, overly enthusiastic, scripted<span class="tok-str">&lt;/Avoid&gt;</span>
  <span class="tok-key">&lt;/Tone&gt;</span>
  <span class="tok-key">&lt;Blacklist&gt;</span>
    <span class="tok-str">&lt;Word&gt;</span>actually<span class="tok-str">&lt;/Word&gt;</span>
    <span class="tok-str">&lt;Word&gt;</span>basically<span class="tok-str">&lt;/Word&gt;</span>
  <span class="tok-key">&lt;/Blacklist&gt;</span>
  <span class="tok-key">&lt;BannedPhrases&gt;</span>
    <span class="tok-str">&lt;Phrase&gt;</span>Here's why you need to act now.<span class="tok-str">&lt;/Phrase&gt;</span>
  <span class="tok-key">&lt;/BannedPhrases&gt;</span>
  <span class="tok-key">&lt;PreferredStyleExamples&gt;</span>
    <span class="tok-str">&lt;Example&gt;</span>Good example text (from positively-rated notes)<span class="tok-str">&lt;/Example&gt;</span>
  <span class="tok-key">&lt;/PreferredStyleExamples&gt;</span>
<span class="tok-key">&lt;/StyleGuide&gt;</span>
        </pre>
      </div>
    </section>

    <!-- CHALLENGES -->
    <section id="challenges">
      <h2>Engineering challenges</h2>

      <div class="challenge-list">
        <div class="challenge">
          <span class="challenge-num">C-01</span>
          <div>
            <div class="challenge-title">Gong & Fathom CORS / iframe restrictions</div>
            <div class="challenge-body">
              Fathom sets <code>X-Frame-Options: sameorigin</code> — can't iframe. Gong uses CDN
              video URLs that block cross-origin XHR. Solution: Puppeteer headless browser scrapes
              the media URL server-side; a custom HLS proxy (<code>/api/hls/m3u8</code> +
              <code>/api/hls/seg</code>) rewrites segment URLs and serves them with correct CORS
              headers. Different Puppeteer runtimes (local vs Vercel serverless) required
              puppeteer-core + @sparticuz/chromium for production.
            </div>
          </div>
        </div>

        <div class="challenge">
          <span class="challenge-num">C-02</span>
          <div>
            <div class="challenge-title">Making GPT match an individual's coaching voice</div>
            <div class="challenge-body">
              Generic "give feedback on this sales call" prompts produce generic output. The solution
              was a versioned multi-file prompt system where each component (persona, task,
              output format, examples) loads independently. Three real transcript-to-notes pairs
              (few-shot XML examples) anchored GPT to the coach's actual style. The Knowledge Base
              XML captures the evolving style guide and is injected at inference time.
            </div>
          </div>
        </div>

        <div class="challenge">
          <span class="challenge-num">C-03</span>
          <div>
            <div class="challenge-title">Lambda cold starts for AI workloads</div>
            <div class="challenge-body">
              GPT-4o report generation averages 60–75s. A cold Lambda start adds 2–5s which
              breaks SSE streaming expectations. Solution: Provisioned Concurrency (5 warm
              instances) on the <code>live</code> alias for the AI Report and Call Notes
              functions. Reserved Concurrency (20) caps cost exposure. The Next.js API route
              surfaces 408 timeout errors as user-friendly messages and supports mid-flight
              cancellation via AbortController.
            </div>
          </div>
        </div>

        <div class="challenge">
          <span class="challenge-num">C-04</span>
          <div>
            <div class="challenge-title">Multi-call context fusion without contradictions</div>
            <div class="challenge-body">
              Generating representative reports across 5 calls with different outcomes risks
              the model producing contradictory insights (e.g., listing something as both a
              Pro and an AOI). The <code>build_multi_call_hybrid_context</code> function
              enforces a call ratio requirement — a pattern must appear in ≥3/5 calls to make
              the report — and explicitly instructs GPT to resolve contradictions in the
              system prompt.
            </div>
          </div>
        </div>

        <div class="challenge">
          <span class="challenge-num">C-05</span>
          <div>
            <div class="challenge-title">Reliable XML output from LLMs</div>
            <div class="challenge-body">
              GPT occasionally produces malformed XML, especially for long outputs. The system
              uses a strict <code>03_output_format.md</code> prompt component, validates the
              XML on parse, and returns a typed <code>502 XML Parsing Failure</code> error
              rather than silently corrupting the report. The graph extraction runs as a
              separate second LLM call to reduce output complexity per request.
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- STACK -->
    <section id="stack">
      <h2>Tech stack</h2>

      <h3>AI / ML layer</h3>
      <div class="chip-group">
        <span class="chip green">GPT-4.1</span>
        <span class="chip green">GPT-4o</span>
        <span class="chip green">Deepgram nova-3</span>
        <span class="chip green">few-shot prompting</span>
        <span class="chip green">XML-structured outputs</span>
        <span class="chip green">versioned prompt system</span>
        <span class="chip green">knowledge base (XML)</span>
        <span class="chip green">RLHF-style feedback loop</span>
      </div>

      <h3>Backend / Infrastructure</h3>
      <div class="chip-group">
        <span class="chip blue">FastAPI</span>
        <span class="chip blue">Mangum (ASGI → Lambda)</span>
        <span class="chip blue">AWS Lambda</span>
        <span class="chip blue">Python 3.13</span>
        <span class="chip blue">Docker (build)</span>
        <span class="chip blue">CloudWatch</span>
        <span class="chip blue">Puppeteer</span>
        <span class="chip blue">hls.js</span>
      </div>

      <h3>Frontend / Full-Stack</h3>
      <div class="chip-group">
        <span class="chip amber">Next.js 14</span>
        <span class="chip amber">TypeScript</span>
        <span class="chip amber">Vercel</span>
        <span class="chip amber">Server-Sent Events (SSE)</span>
        <span class="chip amber">AbortController</span>
        <span class="chip amber">Chart.js</span>
        <span class="chip amber">Notion API</span>
      </div>

      <h3>Data / Auth</h3>
      <div class="chip-group">
        <span class="chip coral">Supabase (Postgres)</span>
        <span class="chip coral">Prisma ORM</span>
        <span class="chip coral">Supabase OAuth</span>
        <span class="chip coral">Supabase Storage</span>
        <span class="chip coral">Notion OAuth</span>
      </div>

      <h3>Architecture tradeoffs considered</h3>
      <table class="tradeoff-table">
        <thead>
          <tr><th>Decision</th><th>Choice made</th><th>Why</th></tr>
        </thead>
        <tbody>
          <tr>
            <td>Prompt structure</td>
            <td>Notes-focused (TRANSCRIPT_WEIGHT=0)</td>
            <td>Structured notes > raw transcript for coherent report reasoning</td>
          </tr>
          <tr>
            <td>Graph generation</td>
            <td>Separate LLM call</td>
            <td>Reduces output complexity; XML parsing failures less likely</td>
          </tr>
          <tr>
            <td>Transcript ingestion</td>
            <td>User-pasted only (never scraped)</td>
            <td>Scraped Gong/Fathom transcripts are unreliable; user paste is stable</td>
          </tr>
          <tr>
            <td>Lambda vs container</td>
            <td>Lambda ZIP (with Docker build)</td>
            <td>Serverless: no idle cost, event-driven; Provisioned Concurrency handles cold starts</td>
          </tr>
          <tr>
            <td>KB compression</td>
            <td>Two modes (enabled/disabled)</td>
            <td>Preserves coach's breadth of feedback while preventing unbounded KB growth</td>
          </tr>
        </tbody>
      </table>
    </section>

    <!-- LEARNINGS -->
    <section id="learnings">
      <h2>Key learnings</h2>

      <div class="callout">
        <p>
          <strong>On prompt engineering at scale:</strong> Modular, versioned prompt files
          are dramatically easier to iterate than monolithic strings. Separating persona,
          task, format, and examples means you can A/B a single component without breaking
          the others. The real prompt engineering challenge isn't writing — it's evaluation.
        </p>
      </div>

      <div class="callout blue">
        <p>
          <strong>On LLM reliability in production:</strong> Never assume the model returns
          valid structured output. Every parse failure needs a typed error, a retry strategy,
          and a graceful UX fallback. The graph extraction running as a separate second call
          was a major reliability improvement over one monolithic output.
        </p>
      </div>

      <div class="callout amber">
        <p>
          <strong>On serverless AI workloads:</strong> Lambda is a strong fit for
          AI microservices — stateless, event-driven, no idle cost. But cold starts
          become a real UX problem at 60–120s latency. Provisioned Concurrency on a
          versioned alias is the right solution, not pre-warming hacks.
        </p>
      </div>

      <p style="margin-top: 1.5rem;">
        This project taught me that building a production AI system is 20% model selection
        and 80% everything else: data ingestion reliability, structured output validation,
        feedback loop design, infrastructure cold-start management, and the deep iterative
        work of aligning model outputs with a real human expert's style.
      </p>
    </section>

  </main>
</div>

<footer>
  <p>Case study · Nevara Call Auditing Tool · Built at <strong>Blue AI Labs</strong> ·
  <a href="https://github.com/getblue-co/call-notes-app/tree/DEV">GitHub (DEV branch)</a></p>
  <p style="margin-top: 6px; color: var(--line2);">
    Note: all proprietary code and data belong to Blue AI Labs. This case study documents architecture and learnings only.
  </p>
</footer>

<script>
  const links = document.querySelectorAll('.sidebar nav a');
  const sections = document.querySelectorAll('section[id]');

  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        links.forEach(l => l.classList.remove('active'));
        const active = document.querySelector(`.sidebar nav a[href="#${entry.target.id}"]`);
        if (active) active.classList.add('active');
      }
    });
  }, { rootMargin: '-20% 0px -70% 0px' });

  sections.forEach(s => observer.observe(s));
</script>

</body>
</html>
