## AXI Handshake Lab Html file

[index.html](https://github.com/user-attachments/files/32155602/index.html)

===================================================


[<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>AXI Handshaking — Student Lecture Notes</title>
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@400;500;600&family=Outfit:wght@400;500;600;700&family=Source+Serif+4:opsz,wght@8..60,400;8..60,600&display=swap" rel="stylesheet" />
<style>
  :root {
    --bg: #0f1419;
    --bg-elev: #1a222c;
    --bg-soft: #243040;
    --ink: #e8eef4;
    --muted: #8b9aab;
    --line: #2e3d4f;
    --master: #3db8a8;
    --master-dim: rgba(61, 184, 168, 0.15);
    --slave: #e8a838;
    --slave-dim: rgba(232, 168, 56, 0.15);
    --ok: #5ecf7a;
    --bad: #e85d5d;
    --stall: #7a8aa0;
    --accent: #4ea8de;
    --code-bg: #0a0e12;
    --radius: 10px;
    --shadow: 0 12px 40px rgba(0,0,0,.35);
    --font: "Outfit", system-ui, sans-serif;
    --serif: "Source Serif 4", Georgia, serif;
    --mono: "IBM Plex Mono", ui-monospace, monospace;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }
  html { scroll-behavior: smooth; }
  body {
    font-family: var(--font);
    background: var(--bg);
    color: var(--ink);
    line-height: 1.65;
    background-image:
      radial-gradient(ellipse 90% 50% at 10% -10%, rgba(61,184,168,.12), transparent 50%),
      radial-gradient(ellipse 70% 40% at 90% 0%, rgba(78,168,222,.08), transparent 45%),
      linear-gradient(180deg, #0f1419 0%, #121820 100%);
    min-height: 100vh;
  }

  .topnav {
    position: sticky; top: 0; z-index: 50;
    backdrop-filter: blur(14px);
    background: rgba(15,20,25,.88);
    border-bottom: 1px solid var(--line);
    padding: .65rem 1rem;
    display: flex; align-items: center; gap: .75rem; flex-wrap: wrap;
  }
  .topnav .brand { font-weight: 700; color: var(--master); white-space: nowrap; font-size: .95rem; }
  .topnav nav { display: flex; gap: .2rem; flex-wrap: wrap; flex: 1; }
  .topnav a {
    color: var(--muted); text-decoration: none;
    font-size: .75rem; padding: .3rem .55rem; border-radius: 6px;
  }
  .topnav a:hover { color: var(--ink); background: var(--bg-soft); }
  .src-link {
    font-size: .72rem; color: var(--accent) !important;
    border: 1px solid rgba(78,168,222,.35); margin-left: auto;
  }

  main { max-width: 900px; margin: 0 auto; padding: 0 1.15rem 5rem; }

  .hero {
    padding: 2.8rem 0 2rem;
    border-bottom: 1px solid var(--line);
    margin-bottom: 2rem;
  }
  .hero-kicker {
    font-size: .78rem; text-transform: uppercase; letter-spacing: .14em;
    color: var(--master); margin-bottom: .7rem; font-weight: 600;
  }
  .hero h1 {
    font-size: clamp(1.85rem, 4.5vw, 2.6rem);
    font-weight: 700; line-height: 1.15; margin-bottom: .85rem;
  }
  .hero-lead {
    font-family: var(--serif);
    font-size: 1.15rem; color: var(--muted);
    max-width: 42ch; margin-bottom: 1.25rem;
  }
  .hero-meta {
    display: flex; gap: .7rem; flex-wrap: wrap;
    font-size: .82rem; color: var(--muted);
  }
  .hero-meta span {
    display: inline-flex; align-items: center; gap: .4rem;
    padding: .3rem .65rem; background: var(--bg-elev);
    border: 1px solid var(--line); border-radius: 999px;
  }
  .dot { width: 8px; height: 8px; border-radius: 50%; display: inline-block; }
  .dot.m { background: var(--master); }
  .dot.s { background: var(--slave); }

  .learning-box {
    background: var(--bg-elev);
    border: 1px solid var(--line);
    border-radius: var(--radius);
    padding: 1.15rem 1.25rem;
    margin: 1.25rem 0 1.75rem;
  }
  .learning-box h3 {
    font-size: .78rem; text-transform: uppercase; letter-spacing: .1em;
    color: var(--accent); margin: 0 0 .6rem; font-weight: 600;
  }
  .learning-box ul { margin: 0; padding-left: 1.2rem; color: #c5d0dc; }
  .learning-box li { margin-bottom: .35rem; }

  section { margin-bottom: 3.25rem; scroll-margin-top: 4rem; }
  section > h2 {
    font-size: 1.45rem; font-weight: 700; margin-bottom: .35rem;
    display: flex; align-items: baseline; gap: .55rem; flex-wrap: wrap;
  }
  section > h2 .num {
    font-family: var(--mono); font-size: .85rem;
    color: var(--master); font-weight: 500;
  }
  .section-sub {
    color: var(--muted); margin-bottom: 1.2rem;
    font-family: var(--serif); font-size: 1.02rem;
  }

  h3 { font-size: 1.08rem; margin: 1.5rem 0 .65rem; font-weight: 600; }
  h4 { font-size: .98rem; margin: 1.1rem 0 .45rem; font-weight: 600; }
  p { margin-bottom: .85rem; color: #c5d0dc; }
  p strong { color: var(--ink); font-weight: 600; }
  ul, ol { margin: 0 0 1rem 1.25rem; color: #c5d0dc; }
  li { margin-bottom: .4rem; }
  a { color: var(--accent); }

  .callout {
    background: var(--bg-elev);
    border-left: 3px solid var(--accent);
    padding: 1rem 1.1rem;
    border-radius: 0 var(--radius) var(--radius) 0;
    margin: 1.15rem 0;
  }
  .callout.warn { border-left-color: var(--bad); }
  .callout.ok { border-left-color: var(--ok); }
  .callout.tip { border-left-color: var(--slave); }
  .callout.student { border-left-color: var(--master); }
  .callout .label {
    font-size: .7rem; text-transform: uppercase; letter-spacing: .1em;
    font-weight: 600; margin-bottom: .3rem;
  }
  .callout.warn .label { color: var(--bad); }
  .callout.ok .label { color: var(--ok); }
  .callout.tip .label { color: var(--slave); }
  .callout.student .label { color: var(--master); }
  .callout .label.default { color: var(--accent); }
  .callout p:last-child { margin-bottom: 0; }

  .analogy {
    display: grid; grid-template-columns: 1fr 1fr; gap: .9rem;
    margin: 1.35rem 0;
  }
  @media (max-width: 640px) { .analogy { grid-template-columns: 1fr; } }
  .analogy-card {
    background: var(--bg-elev);
    border: 1px solid var(--line);
    border-radius: var(--radius);
    padding: 1.1rem;
    position: relative; overflow: hidden;
  }
  .analogy-card::before {
    content: ""; position: absolute; top: 0; left: 0; right: 0; height: 3px;
  }
  .analogy-card.master::before { background: var(--master); }
  .analogy-card.slave::before { background: var(--slave); }
  .analogy-card h4 {
    font-size: .92rem; margin-bottom: .45rem;
    display: flex; align-items: center; gap: .45rem;
  }
  .analogy-card.master h4 { color: var(--master); }
  .analogy-card.slave h4 { color: var(--slave); }
  .analogy-card p { font-size: .9rem; margin: 0; }

  .diagram {
    background: var(--bg-elev);
    border: 1px solid var(--line);
    border-radius: var(--radius);
    padding: 1.25rem;
    margin: 1.35rem 0;
    box-shadow: var(--shadow);
  }
  .diagram figcaption {
    font-size: .8rem; color: var(--muted);
    text-align: center; margin-top: .9rem;
  }
  .diagram svg { width: 100%; height: auto; display: block; }

  .rules { display: flex; flex-direction: column; gap: .75rem; margin: 1.35rem 0; }
  .rule {
    display: grid; grid-template-columns: auto 1fr; gap: .9rem;
    background: var(--bg-elev); border: 1px solid var(--line);
    border-radius: var(--radius); padding: 1rem 1.1rem;
  }
  .rule-num {
    font-family: var(--mono);
    width: 2.1rem; height: 2.1rem;
    display: flex; align-items: center; justify-content: center;
    background: var(--master-dim); color: var(--master);
    border-radius: 8px; font-weight: 600; font-size: .9rem; flex-shrink: 0;
  }
  .rule.rec .rule-num { background: var(--slave-dim); color: var(--slave); }
  .rule h4 { font-size: .95rem; margin: 0 0 .3rem; }
  .rule p { margin: 0; font-size: .9rem; }
  .rule .why {
    margin-top: .55rem; padding-top: .55rem;
    border-top: 1px dashed var(--line);
    font-size: .85rem; color: var(--muted);
  }

  code, .inline-code, p code, li code, td code, h4 code, label code {
    font-family: var(--mono); font-size: .86em;
    background: var(--code-bg); padding: .08em .32em;
    border-radius: 4px; color: var(--master);
  }

  .wave-panel {
    background: var(--bg-elev); border: 1px solid var(--line);
    border-radius: var(--radius); padding: 1.15rem; margin: 1.35rem 0;
  }
  .wave-controls {
    display: flex; gap: .55rem; flex-wrap: wrap; margin-bottom: .9rem; align-items: center;
  }
  .wave-controls button {
    font-family: var(--font); background: var(--bg-soft); color: var(--ink);
    border: 1px solid var(--line); padding: .42rem .85rem; border-radius: 6px;
    cursor: pointer; font-size: .84rem;
  }
  .wave-controls button:hover { border-color: var(--master); background: var(--master-dim); }
  .wave-controls button.primary {
    background: var(--master); color: #0a1210; border-color: var(--master); font-weight: 600;
  }
  .wave-status { margin-left: auto; font-family: var(--mono); font-size: .78rem; color: var(--muted); }
  .wave-status.xfer { color: var(--ok); }
  .wave-status.stall { color: var(--stall); }
  .wave-canvas-wrap {
    overflow-x: auto; background: var(--code-bg); border-radius: 8px; padding: .9rem .4rem .4rem;
  }
  #waveCanvas { display: block; min-width: 640px; }
  .wave-explain {
    margin-top: .9rem; font-size: .88rem; color: var(--muted);
    background: var(--code-bg); border-radius: 8px; padding: .75rem .9rem;
  }
  .wave-explain strong { color: var(--ink); }

  .truth { width: 100%; border-collapse: collapse; margin: 1.1rem 0; font-size: .88rem; }
  .truth th, .truth td {
    border: 1px solid var(--line); padding: .5rem .65rem; text-align: left;
  }
  .truth th { background: var(--bg-soft); font-weight: 600; text-align: center; }
  .truth td:not(:last-child) { text-align: center; }
  .truth td.yes { color: var(--ok); font-weight: 600; }
  .truth td.no { color: var(--muted); }
  .truth tr.highlight { background: rgba(94,207,122,.08); }
  .truth tr.stall-row { background: rgba(232,168,56,.06); }

  .code-block {
    background: var(--code-bg); border: 1px solid var(--line);
    border-radius: var(--radius); margin: 1.15rem 0; overflow: hidden;
  }
  .code-head {
    display: flex; align-items: center; justify-content: space-between; gap: .5rem;
    padding: .5rem .95rem; background: var(--bg-soft);
    border-bottom: 1px solid var(--line); font-size: .76rem; color: var(--muted);
  }
  .code-head .title { color: var(--ink); font-weight: 500; }
  .code-head .lang { font-family: var(--mono); color: var(--master); font-size: .7rem; }
  pre {
    margin: 0; padding: .95rem 1rem; overflow-x: auto;
    font-family: var(--mono); font-size: .74rem; line-height: 1.65; color: #c8d4e0;
  }
  .c-com { color: #6b7c8d; font-style: italic; }
  .c-kw { color: #c792ea; }
  .c-num { color: #f78c6c; }
  .c-sig { color: #82aaff; }
  .c-str { color: #c3e88d; }
  .c-bad { color: #e85d5d; }
  .c-good { color: #5ecf7a; }

  .checklist { list-style: none; display: flex; flex-direction: column; gap: .45rem; margin: 1rem 0; padding: 0; }
  .checklist li {
    background: var(--bg-elev); border: 1px solid var(--line); border-radius: 8px;
    padding: .7rem .95rem; display: grid; grid-template-columns: auto 1fr;
    gap: .7rem; align-items: start; font-size: .9rem; color: #c5d0dc;
  }
  .checklist input[type="checkbox"] {
    width: 1.05rem; height: 1.05rem; margin-top: .15rem;
    accent-color: var(--master); cursor: pointer;
  }

  .steps { display: flex; flex-direction: column; margin: 1.35rem 0; }
  .step {
    display: grid; grid-template-columns: 2.4rem 1fr; gap: .9rem;
    position: relative; padding-bottom: 1.25rem;
  }
  .step:not(:last-child)::before {
    content: ""; position: absolute; left: 1.1rem; top: 2.2rem; bottom: 0;
    width: 2px; background: var(--line);
  }
  .step-badge {
    width: 2.2rem; height: 2.2rem; border-radius: 50%;
    background: var(--master-dim); border: 2px solid var(--master);
    color: var(--master); display: flex; align-items: center; justify-content: center;
    font-family: var(--mono); font-weight: 600; font-size: .82rem; z-index: 1;
  }
  .step h4 { margin: 0 0 .25rem; }
  .step p { margin: 0; font-size: .9rem; }

  .glossary {
    display: grid; gap: .65rem; margin: 1.1rem 0;
  }
  .glossary dt {
    font-family: var(--mono); color: var(--master); font-size: .88rem; font-weight: 600;
  }
  .glossary dd {
    margin: .15rem 0 .55rem; padding-left: .85rem;
    border-left: 2px solid var(--line); color: #c5d0dc; font-size: .9rem;
  }

  .quiz {
    background: var(--bg-elev); border: 1px solid var(--line);
    border-radius: var(--radius); padding: 1.1rem; margin: .9rem 0;
  }
  .quiz h4 { margin: 0 0 .55rem; color: var(--ink); }
  .quiz .opts { display: flex; flex-direction: column; gap: .4rem; margin: .6rem 0; }
  .quiz label {
    display: flex; gap: .55rem; align-items: flex-start;
    background: var(--code-bg); padding: .55rem .7rem; border-radius: 6px;
    cursor: pointer; font-size: .88rem; color: #c5d0dc; border: 1px solid transparent;
  }
  .quiz label:hover { border-color: var(--line); }
  .quiz label.correct { border-color: var(--ok); background: rgba(94,207,122,.08); }
  .quiz label.wrong { border-color: var(--bad); background: rgba(232,93,93,.08); }
  .quiz .feedback {
    font-size: .85rem; margin-top: .5rem; min-height: 1.2em; color: var(--muted);
  }
  .quiz .feedback.show-ok { color: var(--ok); }
  .quiz .feedback.show-bad { color: var(--bad); }
  .quiz button {
    font-family: var(--font); font-size: .82rem; margin-top: .35rem;
    background: var(--bg-soft); color: var(--ink); border: 1px solid var(--line);
    padding: .35rem .75rem; border-radius: 6px; cursor: pointer;
  }

  .cycle-grid {
    display: grid; grid-template-columns: repeat(4, 1fr); gap: .55rem;
    margin: 1.1rem 0;
  }
  @media (max-width: 700px) { .cycle-grid { grid-template-columns: 1fr 1fr; } }
  .cycle-card {
    background: var(--bg-elev); border: 1px solid var(--line);
    border-radius: 8px; padding: .75rem; font-size: .82rem;
  }
  .cycle-card .cyc {
    font-family: var(--mono); font-size: .72rem; color: var(--accent); margin-bottom: .35rem;
  }
  .cycle-card.xfer { border-color: rgba(94,207,122,.45); }
  .cycle-card.stall { border-color: rgba(232,168,56,.4); }

  footer {
    border-top: 1px solid var(--line); padding: 2rem 0;
    text-align: center; color: var(--muted); font-size: .84rem;
  }
  footer a { color: var(--accent); }

  .toc {
    background: var(--bg-elev); border: 1px solid var(--line);
    border-radius: var(--radius); padding: 1.1rem 1.25rem; margin: 1.25rem 0;
  }
  .toc h3 { margin: 0 0 .6rem; font-size: .9rem; color: var(--muted); font-weight: 600; }
  .toc ol { margin: 0; padding-left: 1.2rem; columns: 2; gap: 1.5rem; }
  @media (max-width: 600px) { .toc ol { columns: 1; } }
  .toc li { margin-bottom: .3rem; font-size: .88rem; }
  .toc a { text-decoration: none; }
  .toc a:hover { text-decoration: underline; }

  @media print {
    .topnav { position: static; }
    .wave-controls button, .quiz button { display: none; }
    body { background: #fff; color: #111; }
  }
</style>
</head>
<body>

<header class="topnav">
  <div class="brand">AXI Handshake Lab</div>
  <nav>
    <a href="#start">Start here</a>
    <a href="#basics">Basics</a>
    <a href="#story">Analogy</a>
    <a href="#signals">Signals</a>
    <a href="#rules">Rules</a>
    <a href="#wave">Waveform</a>
    <a href="#slave">Slave</a>
    <a href="#master">Master</a>
    <a href="#bugs">Bugs</a>
    <a href="#formal">Formal</a>
    <a href="#faq">FAQ</a>
    <a href="#quiz">Quiz</a>
    <a href="#glossary">Glossary</a>
  </nav>
  <a class="src-link" href="../axistream/index.html">AXI-Stream lecture →</a>
  <a class="src-link" href="https://zipcpu.com/blog/2021/08/28/axi-rules.html" target="_blank" rel="noopener">ZipCPU source →</a>
</header>

<main>
  <!-- HERO -->
  <header class="hero">
    <p class="hero-kicker">Student lecture notes · SystemVerilog beginners welcome</p>
    <h1>AXI Handshaking, Explained Slowly</h1>
    <p class="hero-lead">
      How two digital blocks agree to pass one piece of data safely —
      with pictures, rules, code, and common mistakes.
    </p>
    <div class="hero-meta">
      <span><i class="dot m"></i> Master = sender</span>
      <span><i class="dot s"></i> Slave = receiver</span>
      <span>Transfer only if VALID ∧ READY</span>
    </div>
  </header>

  <!-- 00 START -->
  <section id="start">
    <h2><span class="num">00</span> How to use this page</h2>
    <p class="section-sub">Read this first if you are a student opening the file for the first time.</p>

    <div class="learning-box">
      <h3>By the end you should be able to</h3>
      <ul>
        <li>Explain what VALID and READY mean in plain English</li>
        <li>Say exactly when a transfer happens (and when it does not)</li>
        <li>Describe what a <em>stall</em> is and why data must stay frozen</li>
        <li>Recognize good vs bad master/slave SystemVerilog patterns</li>
        <li>Spot the classic “TLAST changed while stalled” bug</li>
      </ul>
    </div>

    <div class="toc">
      <h3>Contents</h3>
      <ol>
        <li><a href="#basics">What you need to know first</a></li>
        <li><a href="#story">The package analogy</a></li>
        <li><a href="#signals">The wires (signals)</a></li>
        <li><a href="#rules">The six handshake rules</a></li>
        <li><a href="#wave">Interactive waveform demo</a></li>
        <li><a href="#slave">Writing a slave (receiver)</a></li>
        <li><a href="#master">Writing a master (sender)</a></li>
        <li><a href="#bugs">Famous bugs</a></li>
        <li><a href="#formal">Checking with formal asserts</a></li>
        <li><a href="#faq">FAQ</a></li>
        <li><a href="#quiz">Self-check quiz</a></li>
        <li><a href="#glossary">Glossary</a></li>
      </ol>
    </div>

    <div class="callout student">
      <div class="label">Student tip</div>
      <p>
        Do not skim past Section&nbsp;01. Most confusion about AXI is really confusion about
        <strong>clock cycles</strong>, <strong>who drives which wire</strong>, and what
        “same cycle” means. Those ideas are reviewed there on purpose.
      </p>
    </div>

    <p>
      This page is a teaching rewrite of Dan Gisselquist’s article
      <a href="https://zipcpu.com/blog/2021/08/28/axi-rules.html">AXI Handshaking Rules</a>
      (ZipCPU). The rules are from industry practice / the AXI spec family;
      the explanations here are written for people who know basic SystemVerilog
      (<code>always_ff</code>, <code>logic</code>, clocks, resets) but are new to AXI.
    </p>
  </section>

  <!-- 01 BASICS -->
  <section id="basics">
    <h2><span class="num">01</span> What you need to know first</h2>
    <p class="section-sub">No AXI jargon yet — just the digital design ideas the handshake depends on.</p>

    <h3>1. Everything is timed by a clock</h3>
    <p>
      AXI interfaces share a clock, usually called <code>ACLK</code>.
      On every rising edge of that clock, flip-flops update.
      When we say “this cycle,” we mean <strong>one clock period</strong> —
      the time between two rising edges.
    </p>
    <p>
      A handshake decision (“did we transfer?”) is judged by looking at the
      signal values <strong>during that cycle</strong> (typically sampled on the
      rising edge / as registered values). Beginner rule of thumb:
    </p>
    <div class="callout ok">
      <div class="label">Beginner rule</div>
      <p>
        If <code>VALID</code> and <code>READY</code> are both 1 in the same clock cycle,
        one transfer happens in that cycle. If either is 0, no transfer that cycle.
      </p>
    </div>

    <h3>2. Reset starts things in a known state</h3>
    <p>
      AXI uses an active-low reset, usually <code>ARESETN</code>
      (“N” = negative / active when 0).
      When <code>ARESETN == 0</code>, the system is in reset.
      After reset releases (<code>ARESETN == 1</code>), masters must not pretend
      they already have valid data: <code>VALID</code> must be 0 until they really do.
    </p>

    <h3>3. Who is master? Who is slave?</h3>
    <p>
      These words describe <strong>direction of data for that interface</strong>, not who is “in charge of the chip.”
    </p>
    <ul>
      <li><strong>Master</strong> = the side that <em>sends</em> / offers the payload (drives <code>VALID</code> and data).</li>
      <li><strong>Slave</strong> = the side that <em>receives</em> the payload (drives <code>READY</code>).</li>
    </ul>
    <p>
      One hardware module can be a master on one port and a slave on another.
      Example: a DMA might be an AXI-Stream <em>master</em> when it outputs video,
      and an AXI memory <em>slave</em> when the CPU writes its registers.
    </p>

    <h3>4. Naming you will see in code</h3>
    <p>Xilinx-style prefixes are common:</p>
    <ul>
      <li><code>M_AXIS_TVALID</code> — VALID on a <em>master</em> AXI-Stream port of this module</li>
      <li><code>S_AXIS_TREADY</code> — READY on a <em>slave</em> AXI-Stream port of this module</li>
      <li><code>S_VID_TVALID</code> — VALID on a slave port named “VID” (video)</li>
    </ul>
    <p>
      So: the letter <code>M_</code> / <code>S_</code> tells you the role of <em>that port on this block</em>.
      If your module has an <code>S_AXIS_*</code> port, some other block’s master is talking to you.
    </p>

    <h3>5. What “combinational” vs “registered” means here</h3>
    <p>
      <strong>Registered</strong> = the output comes from a flip-flop (updates on clock edge).
      <strong>Combinational</strong> = output is a pure logic function of inputs right now (no clock delay).
    </p>
    <p>
      AXI requires that there be <strong>no combinatorial path from an interface input to an interface output</strong>
      on master/slave interfaces. In practice: don’t compute <code>READY</code> as a direct combo function of
      <code>VALID</code>/<code>DATA</code> from the other side in a way that creates long combo loops.
      Habit for beginners: <strong>register READY</strong>.
    </p>
  </section>

  <!-- 02 STORY -->
  <section id="story">
    <h2><span class="num">02</span> The package analogy</h2>
    <p class="section-sub">If you remember only one picture, remember this one.</p>

    <div class="analogy">
      <div class="analogy-card master">
        <h4>● Master (sender)</h4>
        <p>
          Raises a hand: <strong>“I have a package for you.”</strong><br />
          That hand is <code>VALID = 1</code>.<br />
          The package contents are <code>DATA</code> (and maybe <code>LAST</code>, <code>USER</code>, …).<br />
          While the hand is up and the other person is not ready, the master must
          <strong>keep holding the same package</strong> — don’t swap it mid-air.
        </p>
      </div>
      <div class="analogy-card slave">
        <h4>● Slave (receiver)</h4>
        <p>
          Raises a hand: <strong>“I can take it now.”</strong><br />
          That hand is <code>READY = 1</code>.<br />
          If the slave is busy, it keeps <code>READY = 0</code> (backpressure).<br />
          The package only moves when <em>both</em> hands are up at once.
        </p>
      </div>
    </div>

    <div class="callout ok">
      <div class="label">The golden rule</div>
      <p>
        A transfer happens in a clock cycle <strong>if and only if</strong>
        <code>VALID && READY</code> is true in that cycle.
        Not “VALID today and READY tomorrow.” Same cycle. Both high.
      </p>
    </div>

    <figure class="diagram" aria-label="Master feeds slave">
      <svg viewBox="0 0 720 210" xmlns="http://www.w3.org/2000/svg" role="img">
        <defs>
          <marker id="arrow" markerWidth="8" markerHeight="8" refX="6" refY="3" orient="auto">
            <path d="M0,0 L6,3 L0,6 Z" fill="#3db8a8"/>
          </marker>
          <marker id="arrow-amber" markerWidth="8" markerHeight="8" refX="6" refY="3" orient="auto">
            <path d="M0,0 L6,3 L0,6 Z" fill="#e8a838"/>
          </marker>
        </defs>
        <rect x="40" y="45" width="160" height="110" rx="12" fill="#1a222c" stroke="#3db8a8" stroke-width="2"/>
        <text x="120" y="95" text-anchor="middle" fill="#3db8a8" font-family="Outfit,sans-serif" font-size="18" font-weight="600">MASTER</text>
        <text x="120" y="118" text-anchor="middle" fill="#8b9aab" font-family="Outfit,sans-serif" font-size="12">offers data</text>
        <rect x="520" y="45" width="160" height="110" rx="12" fill="#1a222c" stroke="#e8a838" stroke-width="2"/>
        <text x="600" y="95" text-anchor="middle" fill="#e8a838" font-family="Outfit,sans-serif" font-size="18" font-weight="600">SLAVE</text>
        <text x="600" y="118" text-anchor="middle" fill="#8b9aab" font-family="Outfit,sans-serif" font-size="12">accepts data</text>
        <line x1="210" y1="75" x2="510" y2="75" stroke="#3db8a8" stroke-width="2" marker-end="url(#arrow)"/>
        <text x="360" y="62" text-anchor="middle" fill="#3db8a8" font-family="IBM Plex Mono,monospace" font-size="12">VALID + DATA (+ LAST…)</text>
        <line x1="510" y1="125" x2="210" y2="125" stroke="#e8a838" stroke-width="2" marker-end="url(#arrow-amber)"/>
        <text x="360" y="148" text-anchor="middle" fill="#e8a838" font-family="IBM Plex Mono,monospace" font-size="12">READY</text>
        <text x="360" y="190" text-anchor="middle" fill="#8b9aab" font-family="Outfit,sans-serif" font-size="13">Both high same cycle ⇒ one beat transfers</text>
      </svg>
      <figcaption>Fig. Data and VALID go master → slave. READY goes slave → master.</figcaption>
    </figure>

    <h3>Four everyday situations</h3>
    <div class="cycle-grid">
      <div class="cycle-card">
        <div class="cyc">VALID=0 READY=0</div>
        <strong>Both idle</strong>
        <p style="margin:.35rem 0 0;font-size:.8rem;">Nobody offering, nobody accepting. No transfer.</p>
      </div>
      <div class="cycle-card">
        <div class="cyc">VALID=0 READY=1</div>
        <strong>Slave waiting</strong>
        <p style="margin:.35rem 0 0;font-size:.8rem;">Receiver is ready, but sender has nothing yet. No transfer.</p>
      </div>
      <div class="cycle-card stall">
        <div class="cyc">VALID=1 READY=0</div>
        <strong>Stall (backpressure)</strong>
        <p style="margin:.35rem 0 0;font-size:.8rem;">Sender offered; receiver busy. Freeze DATA. Keep VALID=1.</p>
      </div>
      <div class="cycle-card xfer">
        <div class="cyc">VALID=1 READY=1</div>
        <strong>Transfer ✓</strong>
        <p style="margin:.35rem 0 0;font-size:.8rem;">Package moves this cycle. Master may offer next beat next cycle.</p>
      </div>
    </div>
  </section>

  <!-- 03 SIGNALS -->
  <section id="signals">
    <h2><span class="num">03</span> The wires (signals)</h2>
    <p class="section-sub">For handshaking we put every signal into one of three buckets.</p>

    <figure class="diagram">
      <svg viewBox="0 0 720 250" xmlns="http://www.w3.org/2000/svg">
        <rect x="30" y="25" width="200" height="195" rx="12" fill="#1a222c" stroke="#3db8a8" stroke-width="1.5"/>
        <text x="130" y="55" text-anchor="middle" fill="#3db8a8" font-family="Outfit" font-size="15" font-weight="600">HANDSHAKE</text>
        <text x="130" y="95" text-anchor="middle" fill="#e8eef4" font-family="IBM Plex Mono" font-size="14">TVALID</text>
        <text x="130" y="125" text-anchor="middle" fill="#e8eef4" font-family="IBM Plex Mono" font-size="14">TREADY</text>
        <text x="130" y="165" text-anchor="middle" fill="#8b9aab" font-family="Outfit" font-size="12">agree whether a</text>
        <text x="130" y="185" text-anchor="middle" fill="#8b9aab" font-family="Outfit" font-size="12">beat moves</text>

        <rect x="260" y="25" width="200" height="195" rx="12" fill="#1a222c" stroke="#4ea8de" stroke-width="1.5"/>
        <text x="360" y="55" text-anchor="middle" fill="#4ea8de" font-family="Outfit" font-size="15" font-weight="600">PAYLOAD</text>
        <text x="360" y="90" text-anchor="middle" fill="#e8eef4" font-family="IBM Plex Mono" font-size="13">TDATA</text>
        <text x="360" y="115" text-anchor="middle" fill="#e8eef4" font-family="IBM Plex Mono" font-size="13">TLAST</text>
        <text x="360" y="140" text-anchor="middle" fill="#e8eef4" font-family="IBM Plex Mono" font-size="13">TUSER / TKEEP…</text>
        <text x="360" y="175" text-anchor="middle" fill="#8b9aab" font-family="Outfit" font-size="12">must stay stable</text>
        <text x="360" y="195" text-anchor="middle" fill="#8b9aab" font-family="Outfit" font-size="12">while stalled</text>

        <rect x="490" y="25" width="200" height="195" rx="12" fill="#1a222c" stroke="#7a8aa0" stroke-width="1.5"/>
        <text x="590" y="55" text-anchor="middle" fill="#7a8aa0" font-family="Outfit" font-size="15" font-weight="600">ALWAYS THERE</text>
        <text x="590" y="105" text-anchor="middle" fill="#e8eef4" font-family="IBM Plex Mono" font-size="14">ACLK</text>
        <text x="590" y="135" text-anchor="middle" fill="#e8eef4" font-family="IBM Plex Mono" font-size="14">ARESETN</text>
        <text x="590" y="180" text-anchor="middle" fill="#8b9aab" font-family="Outfit" font-size="12">clock &amp; reset</text>
      </svg>
      <figcaption>Fig. Minimal stream view. Optional payload wires obey the same freeze-while-stalled rule as TDATA.</figcaption>
    </figure>

    <h3>What each common signal means</h3>
    <table class="truth">
      <thead>
        <tr><th>Signal</th><th>Driven by</th><th>Meaning (plain English)</th></tr>
      </thead>
      <tbody>
        <tr><td><code>ACLK</code></td><td>clock source</td><td>Shared clock for the interface</td></tr>
        <tr><td><code>ARESETN</code></td><td>reset logic</td><td>0 = reset active; 1 = running</td></tr>
        <tr><td><code>TVALID</code></td><td>master</td><td>“My DATA (and friends) are meaningful this cycle”</td></tr>
        <tr><td><code>TREADY</code></td><td>slave</td><td>“I can accept a beat this cycle”</td></tr>
        <tr><td><code>TDATA</code></td><td>master</td><td>The actual data word</td></tr>
        <tr><td><code>TLAST</code></td><td>master</td><td>1 = this beat is the last of a packet</td></tr>
        <tr><td><code>TUSER</code></td><td>master</td><td>Sideband info (e.g. start-of-frame in video)</td></tr>
      </tbody>
    </table>

    <div class="callout tip">
      <div class="label">Notation in the ZipCPU article</div>
      <p>
        <code>xVALID</code> / <code>xREADY</code> means “whatever channel you mean”
        — stream <code>T*</code>, write address <code>AW*</code>, read data <code>R*</code>, etc.
        The handshake idea is the same for AXI-Stream, full AXI, and AXI-Lite.
      </p>
    </div>

    <h3>What is a “beat”?</h3>
    <p>
      One successful handshake transfers <strong>one beat</strong> = one piece of payload
      (one <code>TDATA</code> value, plus associated flags).
      A <strong>packet</strong> is a sequence of beats ending with <code>TLAST=1</code>.
    </p>
  </section>

  <!-- 04 RULES -->
  <section id="rules">
    <h2><span class="num">04</span> The six handshake rules</h2>
    <p class="section-sub">Memorize these. Almost every AXI bug is breaking one of them.</p>

    <div class="rules">
      <article class="rule">
        <div class="rule-num">1</div>
        <div>
          <h4><code>xVALID</code> must be low after reset</h4>
          <p>
            While / after reset, the master must not claim valid data.
            Clear VALID in your reset clause.
          </p>
          <p class="why"><strong>Why:</strong> After reset, the slave assumes no pending offer. A stuck VALID=1 can create a false transfer the moment READY rises.</p>
        </div>
      </article>

      <article class="rule">
        <div class="rule-num">2</div>
        <div>
          <h4>Nothing happens unless <code>xVALID && xREADY</code></h4>
          <p>No transfer. No “almost accepted.” The beat does not move.</p>
          <p class="why"><strong>Why:</strong> This is the definition of the handshake. Both sides must consent.</p>
        </div>
      </article>

      <article class="rule">
        <div class="rule-num">3</div>
        <div>
          <h4>Something <em>always</em> happens when <code>xVALID && xREADY</code></h4>
          <p>
            If both are high, you <strong>accepted</strong> that beat. Capture it, process it, or buffer it.
            Do <em>not</em> write <code>if (VALID && READY && my_flag)</code> and then ignore the beat when <code>my_flag</code> is 0.
          </p>
          <p class="why"><strong>Why:</strong> The other side believes the transfer completed. If you ignore it, that beat is lost forever.</p>
        </div>
      </article>

      <article class="rule">
        <div class="rule-num">4</div>
        <div>
          <h4>Payload may change only when <code>!xVALID || xREADY</code></h4>
          <p>
            While stalled (<code>VALID && !READY</code>): keep VALID=1 and freeze DATA/LAST/USER/….
            Change them only after a transfer, or when VALID is not asserted.
          </p>
          <p class="why"><strong>Why:</strong> The slave might sample DATA whenever VALID is high. Changing DATA mid-stall can make the slave see the wrong value when READY finally rises.</p>
        </div>
      </article>

      <article class="rule">
        <div class="rule-num">5</div>
        <div>
          <h4>No combo path from AXI inputs → outputs; register READY</h4>
          <p>
            Spec idea: interface inputs must not combinationally produce interface outputs.
            Practical habit: register <code>READY</code>. If registering READY hurts throughput, use a <em>skid buffer</em>.
          </p>
          <p class="why"><strong>Why:</strong> Combo paths through READY/VALID can create long timing loops and unstable systems when blocks connect together.</p>
        </div>
      </article>

      <article class="rule rec">
        <div class="rule-num">★</div>
        <div>
          <h4>Recommendation: keep READY high when idle</h4>
          <p>
            Prefer READY=1 whenever you can accept. Lower it only after you accept and need a pause.
            Excellent for streams; a bit harder on some AXI write channels without a skid buffer.
          </p>
          <p class="why"><strong>Why:</strong> READY-default-high often improves throughput and simplifies thinking: “I’m open unless I’m busy.”</p>
        </div>
      </article>
    </div>

    <h3>Truth table (print this / put on the board)</h3>
    <table class="truth">
      <thead>
        <tr>
          <th>VALID</th><th>READY</th><th>What happens?</th><th>May master change DATA?</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>0</td><td>0</td><td class="no">Idle — no transfer</td><td class="yes">Yes (VALID off)</td>
        </tr>
        <tr>
          <td>0</td><td>1</td><td class="no">Slave waiting — no transfer</td><td class="yes">Yes</td>
        </tr>
        <tr class="stall-row">
          <td>1</td><td>0</td><td class="no">STALL — freeze offer</td><td class="no">NO</td>
        </tr>
        <tr class="highlight">
          <td>1</td><td>1</td><td class="yes">TRANSFER this cycle ✓</td><td class="yes">Yes next (new beat / drop VALID)</td>
        </tr>
      </tbody>
    </table>
  </section>

  <!-- 05 WAVE -->
  <section id="wave">
    <h2><span class="num">05</span> See it: interactive waveform</h2>
    <p class="section-sub">Press Play, then read the cycle-by-cycle story under the canvas.</p>

    <div class="wave-panel">
      <div class="wave-controls">
        <button type="button" class="primary" id="btnPlay">Play demo</button>
        <button type="button" id="btnReset">Reset</button>
        <button type="button" id="btnStep">Step 1 cycle</button>
        <span class="wave-status" id="waveStatus">cycle 0 · idle</span>
      </div>
      <div class="wave-canvas-wrap">
        <canvas id="waveCanvas" width="900" height="280" aria-label="AXI handshake waveform"></canvas>
      </div>
      <div class="wave-explain" id="waveExplain">
        Press <strong>Play</strong> or <strong>Step</strong> to walk through a scripted example:
        idle → offer A while stalled → transfer A → transfer B → idle.
      </div>
    </div>

    <h3>What the demo is teaching</h3>
    <ol>
      <li>READY can be high while VALID is low (slave waiting — still no transfer).</li>
      <li>When VALID rises but READY is low, you are stalled: DATA must stay “A”.</li>
      <li>Green <strong>XFER</strong> dots appear only on cycles where both are 1.</li>
      <li>After a transfer, the master may present a new beat (here, “B”) immediately if READY stays high.</li>
    </ol>
  </section>

  <!-- 06 SLAVE -->
  <section id="slave">
    <h2><span class="num">06</span> Writing a slave (receiver)</h2>
    <p class="section-sub">Your job: drive READY, and only consume data on a real handshake.</p>

    <div class="steps">
      <div class="step">
        <div class="step-badge">1</div>
        <div>
          <h4>Decide READY on a clock edge</h4>
          <p>Ask: “Can I accept a beat <em>this coming cycle</em>?” Register that as <code>s_axis_tready</code>.</p>
        </div>
      </div>
      <div class="step">
        <div class="step-badge">2</div>
        <div>
          <h4>Consume with <code>if (VALID && READY)</code> — nothing else</h4>
          <p>
            Extra conditions belong in how you form READY (lower READY when you can’t accept),
            not inside the consume <code>if</code>.
          </p>
        </div>
      </div>
      <div class="step">
        <div class="step-badge">3</div>
        <div>
          <h4>If the handshake fires, you own that beat</h4>
          <p>Store it, process it, or queue it. Do not pretend it didn’t happen.</p>
        </div>
      </div>
    </div>

    <div class="code-block">
      <div class="code-head">
        <span class="title">Canonical AXI-Stream slave (teaching skeleton)</span>
        <span class="lang">SystemVerilog</span>
      </div>
<pre><span class="c-com">// SLAVE: accept a beat only when VALID && READY.
// File also available as: sv/axis_slave_example.sv</span>
<span class="c-kw">module</span> axis_slave_example #(
  <span class="c-kw">parameter int</span> WIDTH = <span class="c-num">32</span>
) (
  <span class="c-kw">input  logic</span>             aclk,
  <span class="c-kw">input  logic</span>             aresetn,
  <span class="c-kw">input  logic</span>             s_axis_tvalid,
  <span class="c-kw">output logic</span>             s_axis_tready,
  <span class="c-kw">input  logic</span> [WIDTH-1:0] s_axis_tdata,
  <span class="c-kw">input  logic</span>             s_axis_tlast,
  <span class="c-kw">output logic</span> [WIDTH-1:0] captured_data,
  <span class="c-kw">output logic</span>             captured_last,
  <span class="c-kw">output logic</span>             beat_pulse
);
  <span class="c-kw">logic</span> holding;  <span class="c-com">// demo backpressure: 1 = still holding last beat</span>

  <span class="c-com">// Rule 5: register READY</span>
  <span class="c-kw">always_ff</span> @(<span class="c-kw">posedge</span> aclk <span class="c-kw">or</span> <span class="c-kw">negedge</span> aresetn) <span class="c-kw">begin</span>
    <span class="c-kw">if</span> (!aresetn) s_axis_tready &lt;= <span class="c-num">1'b0</span>;
    <span class="c-kw">else</span>          s_axis_tready &lt;= !holding;  <span class="c-com">// ★ ready when idle</span>
  <span class="c-kw">end</span>

  <span class="c-kw">always_ff</span> @(<span class="c-kw">posedge</span> aclk <span class="c-kw">or</span> <span class="c-kw">negedge</span> aresetn) <span class="c-kw">begin</span>
    <span class="c-kw">if</span> (!aresetn) <span class="c-kw">begin</span>
      holding &lt;= <span class="c-num">0</span>; captured_data &lt;= <span class="c-str">'0</span>; captured_last &lt;= <span class="c-num">0</span>; beat_pulse &lt;= <span class="c-num">0</span>;
    <span class="c-kw">end</span> <span class="c-kw">else</span> <span class="c-kw">begin</span>
      beat_pulse &lt;= <span class="c-num">0</span>;
      <span class="c-com">// Rules 2 &amp; 3: THE handshake check — do not add extra &amp;&amp; flags</span>
      <span class="c-kw">if</span> (s_axis_tvalid &amp;&amp; s_axis_tready) <span class="c-kw">begin</span>
        captured_data &lt;= s_axis_tdata;
        captured_last &lt;= s_axis_tlast;
        holding       &lt;= <span class="c-num">1</span>;
        beat_pulse    &lt;= <span class="c-num">1</span>;
      <span class="c-kw">end</span>
      <span class="c-com">// Demo only: free slot next quiet cycle</span>
      <span class="c-kw">if</span> (holding &amp;&amp; !(s_axis_tvalid &amp;&amp; s_axis_tready)) holding &lt;= <span class="c-num">0</span>;
    <span class="c-kw">end</span>
  <span class="c-kw">end</span>
<span class="c-kw">endmodule</span></pre>
    </div>

    <div class="callout warn">
      <div class="label">Dangerous pattern</div>
      <p>
        <code>if (s_axis_tvalid &amp;&amp; s_axis_tready &amp;&amp; fifo_not_full)</code>
        — if VALID and READY are both already 1 but the FIFO is full, you still
        <em>protocol-accepted</em> the beat by having READY high, then threw it away in logic.
        Fix: compute READY so it is low when the FIFO is full.
      </p>
    </div>

    <h3>Special case: read and write at once (memory-mapped AXI)</h3>
    <p>
      Some slaves can handle only one of {read, write} at a time.
      If you leave both <code>AWREADY</code> and <code>ARREADY</code> high, both handshakes
      can fire in the same cycle — then you must process <em>both</em> or buffer one.
      If you process neither, you drop requests.
    </p>

    <div class="code-block">
      <div class="code-head">
        <span class="title">Mutual exclusion idea (simplified AXI-Lite)</span>
        <span class="lang">SystemVerilog</span>
      </div>
<pre><span class="c-com">// Accept write only if we are not also accepting a read this cycle</span>
<span class="c-kw">assign</span> <span class="c-sig">axil_write_ready</span> =
    skid_awvalid &amp;&amp; skid_wvalid
 &amp;&amp; (!s_axi_bvalid || s_axi_bready)
 &amp;&amp; !<span class="c-sig">axil_read_ready</span>;

<span class="c-kw">assign</span> <span class="c-sig">axil_read_ready</span> =
    skid_arvalid
 &amp;&amp; (!s_axi_rvalid || s_axi_rready);</pre>
    </div>
  </section>

  <!-- 07 MASTER -->
  <section id="master">
    <h2><span class="num">07</span> Writing a master (sender)</h2>
    <p class="section-sub">Your job: offer beats with VALID+DATA, and freeze them while stalled.</p>

    <div class="callout">
      <div class="label default">Master allow-condition (tattoo this on your brain)</div>
      <p>
        Update <code>VALID</code>, <code>DATA</code>, <code>LAST</code>, … only when
        <code>!VALID || READY</code>.
        That means: “I am not currently sitting in a stall.”
      </p>
    </div>

    <div class="code-block">
      <div class="code-head">
        <span class="title">Canonical AXI-Stream master (ZipCPU form)</span>
        <span class="lang">SystemVerilog</span>
      </div>
<pre><span class="c-com">// MASTER: freeze the offer while VALID &amp;&amp; !READY
// File also available as: sv/axis_master_example.sv</span>
<span class="c-kw">module</span> axis_master_example #(
  <span class="c-kw">parameter int</span> WIDTH = <span class="c-num">32</span>,
  <span class="c-kw">parameter bit</span> OPT_LOWPOWER = <span class="c-num">1'b0</span>
) (
  <span class="c-kw">input  logic</span>             aclk,
  <span class="c-kw">input  logic</span>             aresetn,
  <span class="c-kw">input  logic</span>             next_valid,
  <span class="c-kw">input  logic</span> [WIDTH-1:0] next_data,
  <span class="c-kw">input  logic</span>             next_last,
  <span class="c-kw">output logic</span>             m_axis_tvalid,
  <span class="c-kw">input  logic</span>             m_axis_tready,
  <span class="c-kw">output logic</span> [WIDTH-1:0] m_axis_tdata,
  <span class="c-kw">output logic</span>             m_axis_tlast
);
  <span class="c-com">// Rule 1 + Rule 4</span>
  <span class="c-kw">always_ff</span> @(<span class="c-kw">posedge</span> aclk <span class="c-kw">or</span> <span class="c-kw">negedge</span> aresetn) <span class="c-kw">begin</span>
    <span class="c-kw">if</span> (!aresetn)
      m_axis_tvalid &lt;= <span class="c-num">1'b0</span>;
    <span class="c-kw">else if</span> (!m_axis_tvalid || m_axis_tready)
      m_axis_tvalid &lt;= next_valid;
  <span class="c-kw">end</span>

  <span class="c-com">// Same allow-condition for EVERY payload signal</span>
  <span class="c-kw">always_ff</span> @(<span class="c-kw">posedge</span> aclk <span class="c-kw">or</span> <span class="c-kw">negedge</span> aresetn) <span class="c-kw">begin</span>
    <span class="c-kw">if</span> (OPT_LOWPOWER &amp;&amp; !aresetn) <span class="c-kw">begin</span>
      m_axis_tdata &lt;= <span class="c-str">'0</span>; m_axis_tlast &lt;= <span class="c-num">0</span>;
    <span class="c-kw">end</span> <span class="c-kw">else if</span> (!m_axis_tvalid || m_axis_tready) <span class="c-kw">begin</span>
      m_axis_tdata &lt;= next_data;
      m_axis_tlast &lt;= next_last;
      <span class="c-kw">if</span> (OPT_LOWPOWER &amp;&amp; !next_valid) <span class="c-kw">begin</span>
        m_axis_tdata &lt;= <span class="c-str">'0</span>; m_axis_tlast &lt;= <span class="c-num">0</span>;
      <span class="c-kw">end</span>
    <span class="c-kw">end</span>
    <span class="c-com">// else stalled → hold previous values automatically</span>
  <span class="c-kw">end</span>
<span class="c-kw">endmodule</span></pre>
    </div>

    <figure class="diagram">
      <svg viewBox="0 0 720 200" xmlns="http://www.w3.org/2000/svg">
        <text x="20" y="28" fill="#8b9aab" font-family="Outfit" font-size="13">While stalled (VALID=1, READY=0)…</text>
        <rect x="20" y="45" width="320" height="130" rx="10" fill="#122018" stroke="#5ecf7a" stroke-width="1.5"/>
        <text x="180" y="80" text-anchor="middle" fill="#5ecf7a" font-family="Outfit" font-size="15" font-weight="600">GOOD master</text>
        <text x="180" y="110" text-anchor="middle" fill="#c5d0dc" font-family="IBM Plex Mono" font-size="12">VALID stays 1</text>
        <text x="180" y="135" text-anchor="middle" fill="#c5d0dc" font-family="IBM Plex Mono" font-size="12">DATA / LAST frozen</text>
        <rect x="380" y="45" width="320" height="130" rx="10" fill="#201212" stroke="#e85d5d" stroke-width="1.5"/>
        <text x="540" y="80" text-anchor="middle" fill="#e85d5d" font-family="Outfit" font-size="15" font-weight="600">BAD master</text>
        <text x="540" y="110" text-anchor="middle" fill="#c5d0dc" font-family="IBM Plex Mono" font-size="12">LAST flips early</text>
        <text x="540" y="135" text-anchor="middle" fill="#c5d0dc" font-family="IBM Plex Mono" font-size="12">or DATA changes mid-stall</text>
      </svg>
      <figcaption>Fig. Stall means freeze the offer. Changing LAST/DATA while stalled breaks the protocol.</figcaption>
    </figure>

    <h3>Line-by-line intuition</h3>
    <ul>
      <li><code>if (!aresetn) valid &lt;= 0;</code> — Rule 1.</li>
      <li><code>else if (!valid || ready) valid &lt;= next_valid;</code> — only change the offer when allowed.</li>
      <li>If <code>valid &amp;&amp; !ready</code>, both <code>if</code>s are false → flip-flops hold → freeze. That is Rule 4 for free.</li>
    </ul>
  </section>

  <!-- 08 BUGS -->
  <section id="bugs">
    <h2><span class="num">08</span> Famous bugs (learn by breaking)</h2>
    <p class="section-sub">These are the shapes of mistakes discussed in the ZipCPU article.</p>

    <h3>Bug A — TLAST updates while stalled</h3>
    <p>
      A counter says “next beat is last.” You flop that every cycle without the
      <code>!VALID || READY</code> gate. During a stall on the penultimate beat,
      LAST rises early. Downstream thinks the packet ended too soon.
    </p>

    <div class="code-block">
      <div class="code-head"><span class="title">Broken (anti-pattern)</span><span class="lang">SystemVerilog</span></div>
<pre><span class="c-kw">assign</span> axis_tlast = (read_pointer == NUMBER_OF_ITEMS-<span class="c-num">1</span>);
<span class="c-kw">always_ff</span> @(<span class="c-kw">posedge</span> aclk)
  <span class="c-kw">if</span> (!aresetn) axis_tlast_delay &lt;= <span class="c-num">0</span>;
  <span class="c-kw">else</span>          axis_tlast_delay &lt;= axis_tlast; <span class="c-bad">// missing stall gate!</span>
<span class="c-kw">assign</span> m_axis_tlast = axis_tlast_delay;</pre>
    </div>

    <div class="code-block">
      <div class="code-head"><span class="title">Fixed</span><span class="lang">SystemVerilog</span></div>
<pre><span class="c-kw">always_ff</span> @(<span class="c-kw">posedge</span> aclk)
  <span class="c-kw">if</span> (!aresetn)
    m_axis_tlast &lt;= <span class="c-num">0</span>;
  <span class="c-kw">else if</span> (!m_axis_tvalid || m_axis_tready) <span class="c-good">// freeze while stalled</span>
    m_axis_tlast &lt;= (read_pointer == NUMBER_OF_ITEMS-<span class="c-num">1</span>);</pre>
    </div>

    <h3>Bug B — Update data only on READY (forgetting VALID)</h3>
    <p>
      Conditioning payload updates on <code>READY</code> alone can skip loading the first beat
      when both VALID and READY are low. Use <code>!VALID || READY</code> instead.
    </p>

    <h3>Bug C — AW and AR both fire; you handle them inconsistently</h3>
    <p>
      One piece of logic prefers writes; the FSM prefers reads; burst length is taken from the wrong request.
      Policy must be consistent: mutex READY, or buffer the request you defer, and keep address/length with the request you accepted.
    </p>
  </section>

  <!-- 09 FORMAL -->
  <section id="formal">
    <h2><span class="num">09</span> Formal properties (optional)</h2>
    <p class="section-sub">Turn Rule 1 and Rule 4 into checks a tool (or simulator) can catch.</p>

    <p>
      In one sentence: <strong>if last cycle was stalled, then this cycle VALID must still be 1
      and DATA/LAST must not have changed.</strong>
    </p>

    <div class="code-block">
      <div class="code-head">
        <span class="title">Minimal handshake asserts</span>
        <span class="lang">SystemVerilog · see also sv/axis_handshake_asserts.sv</span>
      </div>
<pre><span class="c-kw">logic</span> f_past_valid;
<span class="c-kw">initial</span> f_past_valid = <span class="c-num">0</span>;
<span class="c-kw">always_ff</span> @(<span class="c-kw">posedge</span> aclk) f_past_valid &lt;= <span class="c-num">1</span>;

<span class="c-kw">always_comb</span>
  <span class="c-kw">if</span> (!f_past_valid) <span class="c-kw">assume</span> (!aresetn);

<span class="c-kw">always_ff</span> @(<span class="c-kw">posedge</span> aclk)
  <span class="c-kw">if</span> (!f_past_valid || $past(!aresetn)) <span class="c-kw">begin</span>
    <span class="c-kw">if</span> (f_past_valid) <span class="c-kw">assert</span> (!m_axis_tvalid);
  <span class="c-kw">end</span> <span class="c-kw">else if</span> ($past(m_axis_tvalid &amp;&amp; !m_axis_tready)) <span class="c-kw">begin</span>
    <span class="c-kw">assert</span> (m_axis_tvalid);
    <span class="c-kw">assert</span> ($stable(m_axis_tdata));
    <span class="c-kw">assert</span> ($stable(m_axis_tlast));
  <span class="c-kw">end</span></pre>
    </div>
  </section>

  <!-- 10 FAQ -->
  <section id="faq">
    <h2><span class="num">10</span> FAQ — questions students actually ask</h2>
    <p class="section-sub">Short answers you can quote in lab.</p>

    <h3>Can VALID and READY both rise in the same cycle?</h3>
    <p>Yes. If both are 1 that cycle, a transfer happens that cycle. That is normal and good.</p>

    <h3>Who is allowed to wait for whom?</h3>
    <p>
      Either side may wait. Master waits by keeping VALID=1 (stall). Slave waits by keeping READY=0.
      There is no rule that says “master must go first” or “slave must go first.”
    </p>

    <h3>Is READY allowed to depend on VALID?</h3>
    <p>
      Carefully. Combinational dependence can create illegal combo paths / loops between blocks.
      Beginner-safe approach: register READY based on your internal “can I accept?” state,
      not a combo function of the master’s VALID/DATA.
    </p>

    <h3>Does this apply only to AXI-Stream?</h3>
    <p>
      No. The same VALID/READY handshake idea appears on AXI and AXI-Lite channels
      (AWVALID/AWREADY, WVALID/WREADY, ARVALID/ARREADY, RVALID/RREADY, BVALID/BREADY).
    </p>

    <h3>What is a skid buffer?</h3>
    <p>
      A tiny (usually 1-deep) elastic buffer that lets you register READY without
      losing a beat when READY falls. It absorbs the “extra” beat that may arrive
      the cycle you decide you are becoming not-ready. Details are a follow-on lecture.
    </p>

    <h3>Why do people say “plus nothing!” on the handshake if?</h3>
    <p>
      Because adding extra terms is the #1 way to drop beats. If wires say the transfer happened,
      your RTL must treat it as happened.
    </p>
  </section>

  <!-- 11 QUIZ -->
  <section id="quiz">
    <h2><span class="num">11</span> Self-check quiz</h2>
    <p class="section-sub">Click an answer, then “Check”. Be honest — this is for you.</p>

    <div class="quiz" data-answer="b">
      <h4>Q1. A transfer occurs when…</h4>
      <div class="opts">
        <label><input type="radio" name="q1" value="a" /> VALID is 1, even if READY is 0</label>
        <label><input type="radio" name="q1" value="b" /> VALID and READY are both 1 in the same cycle</label>
        <label><input type="radio" name="q1" value="c" /> READY is 1, even if VALID is 0</label>
      </div>
      <button type="button" class="check-btn">Check</button>
      <div class="feedback"></div>
    </div>

    <div class="quiz" data-answer="c">
      <h4>Q2. While VALID=1 and READY=0, the master must…</h4>
      <div class="opts">
        <label><input type="radio" name="q2" value="a" /> Drop VALID immediately</label>
        <label><input type="radio" name="q2" value="b" /> Change DATA to the next beat to “get ahead”</label>
        <label><input type="radio" name="q2" value="c" /> Keep VALID=1 and keep DATA/LAST stable</label>
      </div>
      <button type="button" class="check-btn">Check</button>
      <div class="feedback"></div>
    </div>

    <div class="quiz" data-answer="a">
      <h4>Q3. On a slave, which consume check is correct?</h4>
      <div class="opts">
        <label><input type="radio" name="q3" value="a" /> <code>if (valid &amp;&amp; ready)</code> then capture — and form ready so you only assert it when you can</label>
        <label><input type="radio" name="q3" value="b" /> <code>if (valid &amp;&amp; ready &amp;&amp; fifo_not_full)</code> even if ready was already 1</label>
        <label><input type="radio" name="q3" value="c" /> <code>if (valid)</code> alone — ready doesn’t matter</label>
      </div>
      <button type="button" class="check-btn">Check</button>
      <div class="feedback"></div>
    </div>

    <div class="quiz" data-answer="b">
      <h4>Q4. After reset, VALID should be…</h4>
      <div class="opts">
        <label><input type="radio" name="q4" value="a" /> 1, so the slave knows the master is alive</label>
        <label><input type="radio" name="q4" value="b" /> 0, until the master truly has a beat to offer</label>
        <label><input type="radio" name="q4" value="c" /> Equal to READY</label>
      </div>
      <button type="button" class="check-btn">Check</button>
      <div class="feedback"></div>
    </div>

    <div class="callout ok">
      <div class="label">If you remember only three things</div>
      <p>
        ① Transfer ⇔ <code>VALID && READY</code>.
        ② While stalled, freeze the offer.
        ③ Never ignore a handshake that already happened on the wires.
      </p>
    </div>
  </section>

  <!-- 12 GLOSSARY -->
  <section id="glossary">
    <h2><span class="num">12</span> Glossary</h2>
    <p class="section-sub">Quick definitions for when a word feels fuzzy.</p>
    <dl class="glossary">
      <dt>AXI</dt>
      <dd>ARM’s Advanced eXtensible Interface — a family of on-chip bus/stream protocols.</dd>
      <dt>AXI-Stream</dt>
      <dd>Simple unidirectional streaming interface using VALID/READY (+ DATA, optional LAST, …).</dd>
      <dt>Beat</dt>
      <dd>One transferred payload unit (one successful handshake).</dd>
      <dt>Backpressure</dt>
      <dd>Slave sets READY=0 to ask the master to wait.</dd>
      <dt>Stall</dt>
      <dd>VALID=1 and READY=0. Offer is live but not accepted yet; must freeze payload.</dd>
      <dt>Handshake</dt>
      <dd>The agreement moment: VALID and READY both 1 in the same cycle.</dd>
      <dt>Master / Slave</dt>
      <dd>Sender / receiver roles for a given interface port.</dd>
      <dt>Skid buffer</dt>
      <dd>Small buffer that helps register READY without losing throughput/beats.</dd>
      <dt>Payload</dt>
      <dd>Everything that travels with the beat: DATA, LAST, USER, KEEP, …</dd>
      <dt>Registered</dt>
      <dd>Signal comes from a flip-flop (updates on clock).</dd>
    </dl>
  </section>

  <!-- TEACH CHECKLIST -->
  <section id="teach">
    <h2><span class="num">13</span> Instructor checklist</h2>
    <p class="section-sub">If you are teaching from this file, tick as you go.</p>
    <ul class="checklist">
      <li><input type="checkbox" id="c1" /><label for="c1">Review clock cycle + reset (Section 01)</label></li>
      <li><input type="checkbox" id="c2" /><label for="c2">Package analogy + four situations (Section 02)</label></li>
      <li><input type="checkbox" id="c3" /><label for="c3">Draw / show the truth table (Section 04)</label></li>
      <li><input type="checkbox" id="c4" /><label for="c4">Run the waveform; pause on stall cycles (Section 05)</label></li>
      <li><input type="checkbox" id="c5" /><label for="c5">Slave: consume only on VALID&amp;&amp;READY (Section 06)</label></li>
      <li><input type="checkbox" id="c6" /><label for="c6">Master: update only when !VALID || READY (Section 07)</label></li>
      <li><input type="checkbox" id="c7" /><label for="c7">Show TLAST bug then fix (Section 08)</label></li>
      <li><input type="checkbox" id="c8" /><label for="c8">Students attempt quiz (Section 11)</label></li>
    </ul>
  </section>

  <footer>
    Teaching rewrite of
    <a href="https://zipcpu.com/blog/2021/08/28/axi-rules.html">AXI Handshaking Rules</a>
    by Dan Gisselquist (ZipCPU / Gisselquist Technology).<br />
    Open <code>index.html</code> in any browser — no server required.
    Companion SystemVerilog: <code>sv/</code> folder.
  </footer>
</main>

<script>
(function () {
  const canvas = document.getElementById("waveCanvas");
  const ctx = canvas.getContext("2d");
  const statusEl = document.getElementById("waveStatus");
  const explainEl = document.getElementById("waveExplain");

  const script = [
    { v: 0, r: 1, data: "—", note: "Idle. READY is high (slave willing). VALID is low → still no transfer." },
    { v: 0, r: 1, data: "—", note: "Still idle. Slave keeps waiting; master has nothing yet." },
    { v: 1, r: 0, data: "A", note: "Master offers beat A, but READY=0 → STALL. DATA must stay A." },
    { v: 1, r: 0, data: "A", note: "Still stalled. VALID stays 1, DATA frozen at A. (Rule 4)" },
    { v: 1, r: 1, data: "A", note: "READY rises. VALID∧READY → TRANSFER of A. Green XFER mark." },
    { v: 1, r: 1, data: "B", note: "Next beat B offered and accepted immediately (READY stayed high)." },
    { v: 0, r: 1, data: "—", note: "Master drops VALID. Done for now. Slave READY can stay high." },
    { v: 0, r: 1, data: "—", note: "Back to idle. End of demo." },
  ];

  let cycle = 0;
  let timer = null;
  const history = [];

  function pushCycle(i) {
    const s = script[Math.min(i, script.length - 1)];
    history.push({ ...s, xfer: !!(s.v && s.r) });
    if (history.length > 12) history.shift();
  }

  function setStatus(s) {
    statusEl.classList.remove("xfer", "stall");
    if (s.v && s.r) {
      statusEl.textContent = `cycle ${cycle} · TRANSFER data=${s.data}`;
      statusEl.classList.add("xfer");
    } else if (s.v && !s.r) {
      statusEl.textContent = `cycle ${cycle} · STALL (hold data=${s.data})`;
      statusEl.classList.add("stall");
    } else {
      statusEl.textContent = `cycle ${cycle} · idle`;
    }
    explainEl.innerHTML = `<strong>Cycle ${cycle}:</strong> ${s.note}`;
  }

  function draw() {
    const W = canvas.width, H = canvas.height;
    ctx.clearRect(0, 0, W, H);
    const left = 70, right = W - 20;
    const rows = [
      { name: "ACLK", y: 40 },
      { name: "TVALID", y: 95 },
      { name: "TREADY", y: 150 },
      { name: "TDATA", y: 205 },
    ];
    ctx.font = "12px IBM Plex Mono, monospace";
    ctx.fillStyle = "#8b9aab";
    rows.forEach((r) => ctx.fillText(r.name, 8, r.y + 4));

    const n = Math.max(history.length, 1);
    const slot = (right - left) / Math.max(n, 8);

    history.forEach((h, i) => {
      const x0 = left + i * slot;
      const x1 = x0 + slot;
      const cy = rows[0].y;
      ctx.strokeStyle = "#4ea8de";
      ctx.lineWidth = 1.5;
      ctx.beginPath();
      ctx.moveTo(x0, cy + 12);
      ctx.lineTo(x0, cy - 12);
      ctx.lineTo(x0 + slot * 0.45, cy - 12);
      ctx.lineTo(x0 + slot * 0.45, cy + 12);
      ctx.lineTo(x1, cy + 12);
      ctx.stroke();

      function dig(y, val, color, prevKey) {
        const hi = y - 14, lo = y + 14;
        const level = val ? hi : lo;
        ctx.strokeStyle = color;
        ctx.lineWidth = 2;
        ctx.beginPath();
        ctx.moveTo(x0, level);
        ctx.lineTo(x1, level);
        ctx.stroke();
        if (i > 0) {
          const prevVal = history[i - 1][prevKey];
          if (prevVal !== val) {
            ctx.beginPath();
            ctx.moveTo(x0, prevVal ? hi : lo);
            ctx.lineTo(x0, level);
            ctx.stroke();
          }
        }
      }
      dig(rows[1].y, h.v, "#3db8a8", "v");
      dig(rows[2].y, h.r, "#e8a838", "r");

      const dy = rows[3].y;
      ctx.fillStyle = h.v ? "rgba(61,184,168,0.18)" : "rgba(122,138,160,0.08)";
      ctx.fillRect(x0 + 2, dy - 16, slot - 4, 32);
      ctx.strokeStyle = h.v ? "#3db8a8" : "#2e3d4f";
      ctx.strokeRect(x0 + 2, dy - 16, slot - 4, 32);
      ctx.fillStyle = "#e8eef4";
      ctx.font = "13px IBM Plex Mono, monospace";
      ctx.textAlign = "center";
      ctx.fillText(h.data, x0 + slot / 2, dy + 5);
      ctx.textAlign = "left";

      if (h.xfer) {
        ctx.fillStyle = "#5ecf7a";
        ctx.beginPath();
        ctx.arc(x0 + slot / 2, 255, 5, 0, Math.PI * 2);
        ctx.fill();
        ctx.font = "10px Outfit, sans-serif";
        ctx.fillText("XFER", x0 + slot / 2 - 14, 268);
      }
    });
    ctx.fillStyle = "#8b9aab";
    ctx.font = "11px Outfit, sans-serif";
    ctx.fillText("Green dots = successful handshake (VALID ∧ READY)", left, H - 6);
  }

  function reset() {
    clearInterval(timer);
    cycle = 0;
    history.length = 0;
    pushCycle(0);
    setStatus(script[0]);
    draw();
  }

  function step() {
    if (cycle < script.length - 1) cycle++;
    else clearInterval(timer);
    pushCycle(cycle);
    setStatus(script[cycle]);
    draw();
  }

  document.getElementById("btnReset").addEventListener("click", reset);
  document.getElementById("btnStep").addEventListener("click", () => {
    clearInterval(timer);
    step();
  });
  document.getElementById("btnPlay").addEventListener("click", () => {
    reset();
    timer = setInterval(() => {
      if (cycle >= script.length - 1) { clearInterval(timer); return; }
      step();
    }, 850);
  });

  document.querySelectorAll(".checklist input").forEach((box) => {
    const key = "axi-hs-" + box.id;
    box.checked = sessionStorage.getItem(key) === "1";
    box.addEventListener("change", () => sessionStorage.setItem(key, box.checked ? "1" : "0"));
  });

  document.querySelectorAll(".quiz").forEach((quiz) => {
    const answer = quiz.dataset.answer;
    const feedback = quiz.querySelector(".feedback");
    quiz.querySelector(".check-btn").addEventListener("click", () => {
      const selected = quiz.querySelector('input[type="radio"]:checked');
      quiz.querySelectorAll("label").forEach((l) => l.classList.remove("correct", "wrong"));
      if (!selected) {
        feedback.textContent = "Pick an answer first.";
        feedback.className = "feedback show-bad";
        return;
      }
      const label = selected.closest("label");
      if (selected.value === answer) {
        label.classList.add("correct");
        feedback.textContent = "Correct.";
        feedback.className = "feedback show-ok";
      } else {
        label.classList.add("wrong");
        feedback.textContent = "Not quite — re-read the golden rule / stall rule, then try again.";
        feedback.className = "feedback show-bad";
      }
    });
  });

  reset();
})();
</script>
</body>
</html>
Uploading index.html…]()
