## SoC Buses lecture

[index.html](https://github.com/user-attachments/files/32155575/index.html)

========================================================

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>SoC Buses</title>
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link href="https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,500;9..144,700&family=Source+Sans+3:wght@400;600;700&family=JetBrains+Mono:wght@400;600&display=swap" rel="stylesheet" />
<style>
:root {
  --ink: #1a1f2e;
  --ink-soft: #4a5568;
  --paper: #f0ebe3;
  --panel: #fffcf7;
  --line: #d4ccc0;
  --navy: #1e3a5f;
  --steel: #3d6b8c;
  --copper: #c4783a;
  --ok: #2f6b4a;
  --warn: #a63d2f;
  --mono: "JetBrains Mono", ui-monospace, monospace;
  --sans: "Source Sans 3", system-ui, sans-serif;
  --display: "Fraunces", Georgia, serif;
  --radius: 10px;
  --shadow: 0 8px 28px rgba(30, 40, 55, 0.08);
}
* { box-sizing: border-box; margin: 0; padding: 0; }
html { scroll-behavior: smooth; }
body {
  font-family: var(--sans);
  color: var(--ink);
  line-height: 1.6;
  background:
    radial-gradient(1000px 420px at 0% -5%, rgba(30,58,95,.1), transparent 55%),
    radial-gradient(700px 360px at 100% 0%, rgba(196,120,58,.09), transparent 50%),
    linear-gradient(180deg, #e5ddd2 0%, var(--paper) 140px, var(--paper) 100%);
}
a { color: var(--navy); }
code {
  font-family: var(--mono); font-size: .86em;
  background: #e8e2d8; padding: .08em .32em; border-radius: 4px; color: var(--navy);
}

.topbar {
  position: sticky; top: 0; z-index: 40;
  backdrop-filter: blur(12px);
  background: rgba(240,235,227,.92);
  border-bottom: 1px solid var(--line);
}
.topbar-inner {
  max-width: 940px; margin: 0 auto; padding: .65rem 1.1rem;
  display: flex; align-items: center; gap: .75rem; flex-wrap: wrap;
}
.brand {
  font-family: var(--display); font-weight: 700; color: var(--navy);
  white-space: nowrap; font-size: 1.05rem;
}
.nav { display: flex; flex-wrap: wrap; gap: .12rem; flex: 1; }
.nav a {
  text-decoration: none; color: var(--ink-soft);
  font-size: .76rem; padding: .28rem .48rem; border-radius: 6px;
}
.nav a:hover { background: var(--panel); color: var(--ink); }

.wrap { max-width: 940px; margin: 0 auto; padding: 0 1.1rem 4.5rem; }

.hero {
  padding: 2.5rem 0 1.7rem;
  border-bottom: 1px solid var(--line);
  margin-bottom: 2rem;
}
.hero-kicker {
  font-size: .76rem; letter-spacing: .12em; text-transform: uppercase;
  color: var(--copper); font-weight: 700; margin-bottom: .55rem;
}
.hero h1 {
  font-family: var(--display);
  font-size: clamp(2rem, 4.5vw, 2.7rem);
  line-height: 1.12; max-width: 16ch; margin-bottom: .8rem;
}
.hero-lead {
  font-size: 1.15rem; color: var(--ink-soft);
  max-width: 42ch; margin-bottom: 1rem;
}
.pills { display: flex; flex-wrap: wrap; gap: .4rem; }
.pill {
  font-size: .78rem; background: var(--panel); border: 1px solid var(--line);
  padding: .26rem .6rem; border-radius: 999px; color: var(--ink-soft);
}

section { margin-bottom: 2.7rem; scroll-margin-top: 3.5rem; }
.section-head {
  display: flex; align-items: baseline; gap: .65rem;
  margin-bottom: .8rem; flex-wrap: wrap;
}
.section-num { font-family: var(--mono); font-size: .85rem; color: var(--steel); font-weight: 600; }
.section-head h2 {
  font-family: var(--display); font-size: 1.5rem; font-weight: 700; line-height: 1.2;
}
.lede { color: var(--ink-soft); font-size: 1.04rem; margin-bottom: 1rem; max-width: 54ch; }

.card {
  background: var(--panel); border: 1px solid var(--line);
  border-radius: var(--radius); padding: 1.1rem 1.2rem;
  margin: 1rem 0; box-shadow: var(--shadow);
}
.card h3 { font-family: var(--display); font-size: 1.12rem; margin-bottom: .5rem; }
.card p + p { margin-top: .65rem; }
.card ul, .card ol { margin: .5rem 0 .5rem 1.2rem; }
.card li { margin-bottom: .32rem; }

.callout {
  border-left: 3px solid var(--steel);
  background: #e8eef4;
  padding: .85rem 1rem;
  border-radius: 0 8px 8px 0;
  margin: 1rem 0;
}
.callout.warn { border-left-color: var(--warn); background: #f7ebe8; }
.callout.ok { border-left-color: var(--ok); background: #e8f0eb; }
.callout.copper { border-left-color: var(--copper); background: #f7efe6; }
.callout strong {
  display: block; margin-bottom: .2rem; font-size: .75rem;
  text-transform: uppercase; letter-spacing: .08em; color: var(--navy);
}
.callout.warn strong { color: var(--warn); }
.callout.ok strong { color: var(--ok); }
.callout.copper strong { color: var(--copper); }

.two {
  display: grid; grid-template-columns: 1fr 1fr; gap: .85rem; margin: 1rem 0;
}
@media (max-width: 700px) { .two { grid-template-columns: 1fr; } }
.side {
  background: var(--panel); border: 1px solid var(--line);
  border-radius: var(--radius); padding: 1rem; border-top: 3px solid var(--line);
}
.side.bad { border-top-color: var(--warn); }
.side.good { border-top-color: var(--ok); }
.side h4 { font-size: .95rem; margin-bottom: .4rem; }
.side.bad h4 { color: var(--warn); }
.side.good h4 { color: var(--ok); }
.side p { font-size: .9rem; color: var(--ink-soft); margin: 0; }

.diagram {
  background: var(--panel); border: 1px solid var(--line);
  border-radius: var(--radius); padding: 1.1rem; margin: 1rem 0; box-shadow: var(--shadow);
}
.diagram svg { width: 100%; height: auto; display: block; }
.diagram figcaption {
  text-align: center; font-size: .8rem; color: var(--ink-soft); margin-top: .7rem;
}

table.cmp {
  width: 100%; border-collapse: collapse; font-size: .86rem; margin: .7rem 0;
}
table.cmp th, table.cmp td {
  border: 1px solid var(--line); padding: .48rem .55rem; text-align: left; vertical-align: top;
}
table.cmp th { background: #e4ddd3; font-weight: 700; }
table.cmp td:first-child { font-family: var(--mono); font-size: .8rem; color: var(--navy); white-space: nowrap; }
table.cmp .use { color: var(--ok); font-weight: 600; }

.grid3 {
  display: grid; grid-template-columns: repeat(3, 1fr); gap: .7rem; margin: 1rem 0;
}
@media (max-width: 780px) { .grid3 { grid-template-columns: 1fr; } }
.mini {
  background: var(--panel); border: 1px solid var(--line); border-radius: 8px; padding: .85rem;
}
.mini .tag { font-family: var(--mono); font-size: .7rem; color: var(--copper); margin-bottom: .25rem; }
.mini h4 { font-size: .92rem; margin-bottom: .3rem; }
.mini p { font-size: .85rem; color: var(--ink-soft); margin: 0; }

.steps { margin: 1rem 0; }
.step {
  display: grid; grid-template-columns: 2.3rem 1fr; gap: .85rem;
  padding-bottom: 1.05rem; position: relative;
}
.step:not(:last-child)::before {
  content: ""; position: absolute; left: 1.05rem; top: 2.15rem; bottom: 0;
  width: 2px; background: var(--line);
}
.badge {
  width: 2.15rem; height: 2.15rem; border-radius: 50%;
  background: #dfe8f0; border: 2px solid var(--navy);
  color: var(--navy); font-family: var(--mono); font-weight: 700;
  font-size: .82rem; display: flex; align-items: center; justify-content: center; z-index: 1;
}
.step h4 { margin-bottom: .2rem; font-size: 1rem; }
.step p { margin: 0; color: var(--ink-soft); font-size: .92rem; }

.arb {
  background: var(--panel); border: 1px solid var(--line);
  border-radius: var(--radius); padding: 1rem; margin: 1rem 0; box-shadow: var(--shadow);
}
.arb-controls {
  display: flex; flex-wrap: wrap; gap: .5rem; align-items: center; margin-bottom: .75rem;
}
.arb-controls button {
  font-family: var(--sans); font-size: .84rem;
  border: 1px solid var(--line); background: #f7f3ec;
  padding: .38rem .75rem; border-radius: 6px; cursor: pointer; color: var(--ink);
}
.arb-controls button:hover { border-color: var(--navy); background: #e8eef4; }
.arb-controls button.primary {
  background: var(--navy); color: #fff; border-color: var(--navy); font-weight: 700;
}
.arb-controls select {
  font-family: var(--sans); font-size: .84rem; padding: .35rem .5rem;
  border: 1px solid var(--line); border-radius: 6px; background: #fff;
}
.arb-status { margin-left: auto; font-family: var(--mono); font-size: .78rem; color: var(--ink-soft); }
.masters {
  display: grid; grid-template-columns: repeat(3, 1fr); gap: .55rem; margin-bottom: .75rem;
}
@media (max-width: 600px) { .masters { grid-template-columns: 1fr; } }
.mcard {
  border: 1px solid var(--line); border-radius: 8px; padding: .7rem;
  background: #f7f3ec; transition: border-color .2s, background .2s;
}
.mcard.active { border-color: var(--ok); background: #e8f0eb; }
.mcard.waiting { border-color: var(--copper); background: #f7efe6; }
.mcard h4 { font-family: var(--mono); font-size: .82rem; margin-bottom: .25rem; }
.mcard p { font-size: .8rem; color: var(--ink-soft); margin: 0; }
.bus-rail {
  background: #1a1f2e; color: #e8e2d8; border-radius: 8px;
  padding: .85rem 1rem; font-family: var(--mono); font-size: .82rem;
  min-height: 3.2rem; display: flex; align-items: center;
}
.bus-rail .grant { color: #7dcea0; }
.bus-rail .idle { color: #8a9099; }

.decision {
  display: grid; gap: .55rem; margin: 1rem 0;
}
.decision .row {
  display: grid; grid-template-columns: 1fr auto; gap: .75rem;
  align-items: center; background: var(--panel); border: 1px solid var(--line);
  border-radius: 8px; padding: .75rem 1rem;
}
.decision .q { font-size: .92rem; }
.decision .a {
  font-family: var(--mono); font-size: .78rem; color: var(--navy);
  background: #e4ddd3; padding: .3rem .55rem; border-radius: 6px; white-space: nowrap;
}
@media (max-width: 600px) {
  .decision .row { grid-template-columns: 1fr; }
  .decision .a { justify-self: start; }
}

.qa details {
  background: var(--panel); border: 1px solid var(--line);
  border-radius: 8px; padding: .75rem 1rem; margin: .45rem 0;
}
.qa summary {
  cursor: pointer; font-weight: 700; list-style: none;
}
.qa summary::-webkit-details-marker { display: none; }
.qa summary::before { content: "▸ "; color: var(--steel); }
.qa details[open] summary::before { content: "▾ "; }
.qa details p { margin-top: .5rem; color: var(--ink-soft); font-size: .92rem; }

footer {
  border-top: 1px solid var(--line); padding: 1.75rem 0 0; margin-top: 1rem;
  text-align: center; color: var(--ink-soft); font-size: .84rem;
}

@media print {
  .topbar { position: static; }
  .arb-controls button { display: none; }
}
</style>
</head>
<body>

<header class="topbar">
  <div class="topbar-inner">
    <div class="brand">SoC Buses</div>
    <nav class="nav" aria-label="Sections">
      <a href="#why">Why</a>
      <a href="#anatomy">Anatomy</a>
      <a href="#transaction">Transaction</a>
      <a href="#arb">Arbitration</a>
      <a href="#demo">Demo</a>
      <a href="#menu">Bus menu</a>
      <a href="#when">When to use what</a>
      <a href="#modern">Interconnects</a>
      <a href="#qa">Q&amp;A</a>
    </nav>
  </div>
</header>

<main class="wrap">

  <header class="hero">
    <p class="hero-kicker">System-on-Chip · shared roads for data</p>
    <h1>Why chips need buses</h1>
    <p class="hero-lead">
      A CPU, a DMA, a camera, and a memory controller all want to talk.
      Without a shared interconnect, the chip becomes a knot of point-to-point wires.
    </p>
    <div class="pills">
      <span class="pill">Masters request · Slaves respond</span>
      <span class="pill">Arbiter picks the winner</span>
      <span class="pill">Pick the bus to match the traffic</span>
    </div>
  </header>

  <!-- 01 WHY -->
  <section id="why">
    <div class="section-head">
      <span class="section-num">01</span>
      <h2>The wiring problem</h2>
    </div>
    <p class="lede">
      Same story as a city: every house with a private road to every shop does not scale.
      Chips hit that wall early.
    </p>

    <div class="two">
      <div class="side bad">
        <h4>Point-to-point everywhere</h4>
        <p>
          N masters × M slaves ⇒ up to N·M dedicated links.
          Each link has its own width, protocol, and timing closure problem.
          Adding one new peripheral means rewiring half the design.
        </p>
      </div>
      <div class="side good">
        <h4>Shared bus / interconnect</h4>
        <p>
          Everyone speaks a common protocol to a shared fabric.
          New IP plugs in at a standard port. Address map decides
          <em>who</em> you reach; the fabric decides <em>when</em> you get the road.
        </p>
      </div>
    </div>

    <figure class="diagram">
      <svg viewBox="0 0 900 280" xmlns="http://www.w3.org/2000/svg" role="img">
        <!-- Left: spaghetti -->
        <text x="200" y="28" text-anchor="middle" fill="#a63d2f" font-family="Fraunces,Georgia,serif" font-size="16" font-weight="700">Without a bus</text>
        <rect x="40" y="55" width="70" height="36" rx="6" fill="#fffcf7" stroke="#a63d2f" stroke-width="1.5"/>
        <text x="75" y="78" text-anchor="middle" fill="#1a1f2e" font-family="JetBrains Mono,monospace" font-size="11">CPU</text>
        <rect x="40" y="110" width="70" height="36" rx="6" fill="#fffcf7" stroke="#a63d2f" stroke-width="1.5"/>
        <text x="75" y="133" text-anchor="middle" fill="#1a1f2e" font-family="JetBrains Mono,monospace" font-size="11">DMA</text>
        <rect x="40" y="165" width="70" height="36" rx="6" fill="#fffcf7" stroke="#a63d2f" stroke-width="1.5"/>
        <text x="75" y="188" text-anchor="middle" fill="#1a1f2e" font-family="JetBrains Mono,monospace" font-size="11">GPU</text>

        <rect x="290" y="55" width="70" height="36" rx="6" fill="#fffcf7" stroke="#4a5568" stroke-width="1.5"/>
        <text x="325" y="78" text-anchor="middle" fill="#1a1f2e" font-family="JetBrains Mono,monospace" font-size="11">RAM</text>
        <rect x="290" y="110" width="70" height="36" rx="6" fill="#fffcf7" stroke="#4a5568" stroke-width="1.5"/>
        <text x="325" y="133" text-anchor="middle" fill="#1a1f2e" font-family="JetBrains Mono,monospace" font-size="11">UART</text>
        <rect x="290" y="165" width="70" height="36" rx="6" fill="#fffcf7" stroke="#4a5568" stroke-width="1.5"/>
        <text x="325" y="188" text-anchor="middle" fill="#1a1f2e" font-family="JetBrains Mono,monospace" font-size="11">SPI</text>

        <path d="M110,73 C170,73 200,73 290,73" fill="none" stroke="#a63d2f" stroke-width="1.2" opacity=".7"/>
        <path d="M110,73 C160,73 200,128 290,128" fill="none" stroke="#a63d2f" stroke-width="1.2" opacity=".55"/>
        <path d="M110,73 C150,73 210,183 290,183" fill="none" stroke="#a63d2f" stroke-width="1.2" opacity=".4"/>
        <path d="M110,128 C170,128 200,73 290,73" fill="none" stroke="#c4783a" stroke-width="1.2" opacity=".7"/>
        <path d="M110,128 C170,128 200,128 290,128" fill="none" stroke="#c4783a" stroke-width="1.2" opacity=".55"/>
        <path d="M110,128 C160,128 210,183 290,183" fill="none" stroke="#c4783a" stroke-width="1.2" opacity=".4"/>
        <path d="M110,183 C170,183 200,73 290,73" fill="none" stroke="#3d6b8c" stroke-width="1.2" opacity=".55"/>
        <path d="M110,183 C170,183 200,128 290,128" fill="none" stroke="#3d6b8c" stroke-width="1.2" opacity=".45"/>
        <path d="M110,183 C170,183 210,183 290,183" fill="none" stroke="#3d6b8c" stroke-width="1.2" opacity=".7"/>
        <text x="200" y="240" text-anchor="middle" fill="#4a5568" font-family="Source Sans 3,sans-serif" font-size="12">9 dedicated links · grows as N×M</text>

        <!-- Right: bus -->
        <text x="680" y="28" text-anchor="middle" fill="#2f6b4a" font-family="Fraunces,Georgia,serif" font-size="16" font-weight="700">With a shared fabric</text>
        <rect x="480" y="55" width="70" height="36" rx="6" fill="#fffcf7" stroke="#1e3a5f" stroke-width="1.5"/>
        <text x="515" y="78" text-anchor="middle" fill="#1a1f2e" font-family="JetBrains Mono,monospace" font-size="11">CPU</text>
        <rect x="480" y="110" width="70" height="36" rx="6" fill="#fffcf7" stroke="#1e3a5f" stroke-width="1.5"/>
        <text x="515" y="133" text-anchor="middle" fill="#1a1f2e" font-family="JetBrains Mono,monospace" font-size="11">DMA</text>
        <rect x="480" y="165" width="70" height="36" rx="6" fill="#fffcf7" stroke="#1e3a5f" stroke-width="1.5"/>
        <text x="515" y="188" text-anchor="middle" fill="#1a1f2e" font-family="JetBrains Mono,monospace" font-size="11">GPU</text>

        <rect x="600" y="70" width="100" height="120" rx="10" fill="#1e3a5f"/>
        <text x="650" y="125" text-anchor="middle" fill="#fffcf7" font-family="Fraunces,Georgia,serif" font-size="14" font-weight="700">BUS /</text>
        <text x="650" y="145" text-anchor="middle" fill="#fffcf7" font-family="Fraunces,Georgia,serif" font-size="14" font-weight="700">NoC</text>

        <rect x="750" y="55" width="70" height="36" rx="6" fill="#fffcf7" stroke="#4a5568" stroke-width="1.5"/>
        <text x="785" y="78" text-anchor="middle" fill="#1a1f2e" font-family="JetBrains Mono,monospace" font-size="11">RAM</text>
        <rect x="750" y="110" width="70" height="36" rx="6" fill="#fffcf7" stroke="#4a5568" stroke-width="1.5"/>
        <text x="785" y="133" text-anchor="middle" fill="#1a1f2e" font-family="JetBrains Mono,monospace" font-size="11">UART</text>
        <rect x="750" y="165" width="70" height="36" rx="6" fill="#fffcf7" stroke="#4a5568" stroke-width="1.5"/>
        <text x="785" y="188" text-anchor="middle" fill="#1a1f2e" font-family="JetBrains Mono,monospace" font-size="11">SPI</text>

        <line x1="550" y1="73" x2="600" y2="100" stroke="#1e3a5f" stroke-width="2"/>
        <line x1="550" y1="128" x2="600" y2="130" stroke="#1e3a5f" stroke-width="2"/>
        <line x1="550" y1="183" x2="600" y2="160" stroke="#1e3a5f" stroke-width="2"/>
        <line x1="700" y1="100" x2="750" y2="73" stroke="#3d6b8c" stroke-width="2"/>
        <line x1="700" y1="130" x2="750" y2="128" stroke="#3d6b8c" stroke-width="2"/>
        <line x1="700" y1="160" x2="750" y2="183" stroke="#3d6b8c" stroke-width="2"/>
        <text x="680" y="240" text-anchor="middle" fill="#4a5568" font-family="Source Sans 3,sans-serif" font-size="12">Standard ports · address map · one arbiter (or many)</text>
      </svg>
      <figcaption>Fig. Buses exist so IP can plug in without rewriting the whole chip’s wiring.</figcaption>
    </figure>

    <div class="grid3">
      <div class="mini">
        <div class="tag">SCALE</div>
        <h4>More blocks, same protocol</h4>
        <p>SoCs grow by instantiating IP. A bus is the socket those blocks share.</p>
      </div>
      <div class="mini">
        <div class="tag">ORDER</div>
        <h4>Who goes when</h4>
        <p>Two masters cannot own the same wires at once. Arbitration is traffic control.</p>
      </div>
      <div class="mini">
        <div class="tag">MAP</div>
        <h4>Address → device</h4>
        <p>CPU writes <code>0x4000_1000</code>; decode logic steers that to the UART, not to DRAM.</p>
      </div>
    </div>
  </section>

  <!-- 02 ANATOMY -->
  <section id="anatomy">
    <div class="section-head">
      <span class="section-num">02</span>
      <h2>Anatomy of a bus</h2>
    </div>
    <p class="lede">
      Strip the acronyms. A memory-mapped bus is a contract about requests, grants, and responses.
    </p>

    <div class="card">
      <h3>Cast of characters</h3>
      <ul>
        <li><strong>Master</strong> — initiates transfers (CPU core, DMA, GPU, Ethernet MAC).</li>
        <li><strong>Slave</strong> — responds to transfers (SRAM, DRAM controller, peripheral registers).</li>
        <li><strong>Arbiter</strong> — when several masters want the bus, picks one.</li>
        <li><strong>Decoder / interconnect</strong> — routes a transaction to the right slave by address (or by stream destination).</li>
      </ul>
      <p>
        One physical block can be both: a DMA is a master toward memory and often a slave
        toward the CPU (so software can program its descriptors).
      </p>
    </div>

    <div class="card">
      <h3>What travels on the wires (conceptually)</h3>
      <table class="cmp">
        <thead>
          <tr><th>Kind of info</th><th>Examples</th></tr>
        </thead>
        <tbody>
          <tr><td>Control</td><td>Read vs write, start of transfer, burst length, byte strobes</td></tr>
          <tr><td>Address</td><td>Where in the memory map</td></tr>
          <tr><td>Data</td><td>Write data outbound, read data inbound</td></tr>
          <tr><td>Handshake / response</td><td>Ready, valid, OKAY / ERROR / RETRY</td></tr>
          <tr><td>Sideband</td><td>Cache attributes, security (TrustZone), QoS, user bits</td></tr>
        </tbody>
      </table>
    </div>

    <div class="callout copper">
      <strong>Pipeline parallel</strong>
      A bus transaction is like an instruction that leaves the core and comes back with a result —
      except the “pipeline” runs across chips blocks, and several outstanding transactions may be in flight.
    </div>
  </section>

  <!-- 03 TRANSACTION -->
  <section id="transaction">
    <div class="section-head">
      <span class="section-num">03</span>
      <h2>Life of one transaction</h2>
    </div>
    <p class="lede">Memory-mapped read, told as a story. Details differ by protocol; the plot does not.</p>

    <div class="steps">
      <div class="step">
        <div class="badge">1</div>
        <div>
          <h4>Master wants something</h4>
          <p>CPU needs a load from <code>0x2000_0040</code>. It asserts a request toward the fabric.</p>
        </div>
      </div>
      <div class="step">
        <div class="badge">2</div>
        <div>
          <h4>Arbiter grants the master</h4>
          <p>If the DMA is mid-burst, the CPU may wait. When granted, the master’s request is on the shared path.</p>
        </div>
      </div>
      <div class="step">
        <div class="badge">3</div>
        <div>
          <h4>Decode steers to a slave</h4>
          <p>Address range <code>0x2000_0000–0x2000_FFFF</code> → on-chip SRAM. UART is not involved.</p>
        </div>
      </div>
      <div class="step">
        <div class="badge">4</div>
        <div>
          <h4>Slave responds</h4>
          <p>SRAM returns data (and an OKAY). Fabric routes the response back to the requesting master.</p>
        </div>
      </div>
      <div class="step">
        <div class="badge">5</div>
        <div>
          <h4>Master completes</h4>
          <p>Load data lands in a register. Bus is free for the next grant — or already serving another outstanding request on a split/multi-channel protocol.</p>
        </div>
      </div>
    </div>

    <div class="two">
      <div class="card" style="margin:0">
        <h3>Shared bus (classic)</h3>
        <p>
          One set of address/data wires. One master owns them at a time.
          Simple, cheap, contention-heavy under load. Think old AHB / Wishbone shared.
        </p>
      </div>
      <div class="card" style="margin:0">
        <h3>Crossbar / NoC (modern SoC)</h3>
        <p>
          Multiple paths. CPU→UART and DMA→DRAM can run in parallel if routes don’t collide.
          Higher throughput, more silicon, more interesting QoS.
        </p>
      </div>
    </div>
  </section>

  <!-- 04 ARBITRATION -->
  <section id="arb">
    <div class="section-head">
      <span class="section-num">04</span>
      <h2>Arbitration — who gets the road</h2>
    </div>
    <p class="lede">
      When two masters request in the same cycle, someone must win.
      The policy is a design choice with real latency and fairness consequences.
    </p>

    <div class="grid3">
      <div class="mini">
        <div class="tag">FIXED PRIORITY</div>
        <h4>Always prefer master 0</h4>
        <p>CPU beats DMA beats debug. Simple. Starvation risk for low-priority masters.</p>
      </div>
      <div class="mini">
        <div class="tag">ROUND-ROBIN</div>
        <h4>Take turns</h4>
        <p>After a grant, that master goes to the back of the line. Fair under sustained load.</p>
      </div>
      <div class="mini">
        <div class="tag">WEIGHTED / QoS</div>
        <h4>Not all traffic equal</h4>
        <p>Video DMA gets guaranteed slots; CPU gets low latency; background copy waits.</p>
      </div>
    </div>

    <div class="card">
      <h3>Policies you will hear about</h3>
      <table class="cmp">
        <thead>
          <tr><th>Policy</th><th>Behavior</th><th>Watch out for</th></tr>
        </thead>
        <tbody>
          <tr>
            <td>Fixed priority</td>
            <td>Highest requesting master always wins</td>
            <td>Low-priority starvation</td>
          </tr>
          <tr>
            <td>Round-robin</td>
            <td>Rotate among requesters</td>
            <td>Can hurt a latency-critical CPU if everyone is chatty</td>
          </tr>
          <tr>
            <td>LRU / fair</td>
            <td>Prefer who waited longest</td>
            <td>Slightly more state in the arbiter</td>
          </tr>
          <tr>
            <td>Time-division / TDM</td>
            <td>Slots reserved on a schedule</td>
            <td>Wastes bandwidth if a slot’s owner is idle</td>
          </tr>
          <tr>
            <td>QoS / credit</td>
            <td>Urgency tags, bandwidth budgets</td>
            <td>Complexity — common in big application SoCs</td>
          </tr>
        </tbody>
      </table>
    </div>

    <div class="callout">
      <strong>Burst note</strong>
      Many protocols let a master keep the bus for a burst (several beats) once granted,
      so DRAM page opens aren’t wasted. Arbitration often happens between bursts, not every beat —
      unless the fabric is multi-issue / multi-channel (AXI).
    </div>
  </section>

  <!-- 05 DEMO -->
  <section id="demo">
    <div class="section-head">
      <span class="section-num">05</span>
      <h2>Watch an arbiter choose</h2>
    </div>
    <p class="lede">Three masters request the bus. Switch policy and step cycle by cycle.</p>

    <div class="arb">
      <div class="arb-controls">
        <label>
          Policy
          <select id="policy">
            <option value="priority">Fixed priority (CPU > DMA > GPU)</option>
            <option value="rr">Round-robin</option>
          </select>
        </label>
        <button type="button" class="primary" id="btnStep">Step cycle</button>
        <button type="button" id="btnAuto">Auto-run</button>
        <button type="button" id="btnReset">Reset</button>
        <span class="arb-status" id="arbStatus">cycle 0</span>
      </div>
      <div class="masters" id="masterCards">
        <div class="mcard" id="m0"><h4>M0 CPU</h4><p>priority highest</p></div>
        <div class="mcard" id="m1"><h4>M1 DMA</h4><p>mid priority</p></div>
        <div class="mcard" id="m2"><h4>M2 GPU</h4><p>priority lowest</p></div>
      </div>
      <div class="bus-rail" id="busRail"><span class="idle">bus idle — press Step</span></div>
      <p style="margin-top:.7rem;font-size:.85rem;color:var(--ink-soft);">
        Scripted request pattern: who wants the bus each cycle is fixed so you can compare policies on the same traffic.
      </p>
    </div>
  </section>

  <!-- 06 MENU -->
  <section id="menu">
    <div class="section-head">
      <span class="section-num">06</span>
      <h2>The bus menu</h2>
    </div>
    <p class="lede">
      Real SoCs mix several protocols. Each one optimizes a different kind of traffic.
    </p>

    <div class="card">
      <h3>ARM / AMBA family (very common in class &amp; industry)</h3>
      <table class="cmp">
        <thead>
          <tr><th>Bus</th><th>Personality</th><th>Typical use</th></tr>
        </thead>
        <tbody>
          <tr>
            <td>APB</td>
            <td>Low speed, simple, two-cycle-ish register access</td>
            <td class="use">UART, GPIO, timers, config regs</td>
          </tr>
          <tr>
            <td>AHB / AHB-Lite</td>
            <td>Single shared pipelined bus, moderate performance</td>
            <td class="use">Small MCUs, on-chip SRAM, simple DMA</td>
          </tr>
          <tr>
            <td>AXI</td>
            <td>High performance, separate channels, bursts, outstanding txns</td>
            <td class="use">CPU↔DRAM, GPU, high-end DMA</td>
          </tr>
          <tr>
            <td>AXI-Lite</td>
            <td>AXI subset: no bursts, simpler slaves</td>
            <td class="use">Control/status registers on an AXI fabric</td>
          </tr>
          <tr>
            <td>AXI-Stream</td>
            <td>No address — unidirectional data flow + handshake</td>
            <td class="use">Video, DSP, packet pipelines</td>
          </tr>
        </tbody>
      </table>
    </div>

    <div class="card">
      <h3>Other names you will meet</h3>
      <table class="cmp">
        <thead>
          <tr><th>Bus / fabric</th><th>Where it shows up</th><th>Notes</th></tr>
        </thead>
        <tbody>
          <tr>
            <td>Wishbone</td>
            <td>Open-source FPGA / Libre SoCs</td>
            <td>Simple classic shared bus; easy to learn</td>
          </tr>
          <tr>
            <td>Avalon (MM / ST)</td>
            <td>Intel/Altera FPGA tools</td>
            <td>Memory-mapped + stream cousins of AXI / AXIS</td>
          </tr>
          <tr>
            <td>TileLink</td>
            <td>RISC-V / SiFive / Rocket Chip world</td>
            <td>Cache-coherent friendly</td>
          </tr>
          <tr>
            <td>Chi / ACE</td>
            <td>Big coherent CPU clusters</td>
            <td>Coherency protocol on top of / beside AXI ideas</td>
          </tr>
          <tr>
            <td>PCIe / CXL</td>
            <td>Off-chip / between chips</td>
            <td>Not an on-chip SoC bus, but the “outside world” cousin</td>
          </tr>
        </tbody>
      </table>
    </div>

    <figure class="diagram">
      <svg viewBox="0 0 900 260" xmlns="http://www.w3.org/2000/svg" role="img">
        <text x="450" y="28" text-anchor="middle" fill="#1e3a5f" font-family="Fraunces,Georgia,serif" font-size="16" font-weight="700">A typical layered SoC (simplified)</text>

        <rect x="60" y="50" width="100" height="50" rx="8" fill="#fffcf7" stroke="#1e3a5f" stroke-width="1.5"/>
        <text x="110" y="80" text-anchor="middle" fill="#1a1f2e" font-family="JetBrains Mono,monospace" font-size="12">CPU</text>
        <rect x="180" y="50" width="100" height="50" rx="8" fill="#fffcf7" stroke="#1e3a5f" stroke-width="1.5"/>
        <text x="230" y="80" text-anchor="middle" fill="#1a1f2e" font-family="JetBrains Mono,monospace" font-size="12">DMA</text>
        <rect x="300" y="50" width="100" height="50" rx="8" fill="#fffcf7" stroke="#1e3a5f" stroke-width="1.5"/>
        <text x="350" y="80" text-anchor="middle" fill="#1a1f2e" font-family="JetBrains Mono,monospace" font-size="12">GPU</text>

        <rect x="60" y="120" width="340" height="44" rx="8" fill="#1e3a5f"/>
        <text x="230" y="147" text-anchor="middle" fill="#fffcf7" font-family="Source Sans 3,sans-serif" font-size="14" font-weight="700">AXI interconnect (high bandwidth)</text>

        <rect x="60" y="185" width="100" height="44" rx="8" fill="#fffcf7" stroke="#3d6b8c" stroke-width="1.5"/>
        <text x="110" y="212" text-anchor="middle" fill="#1a1f2e" font-family="JetBrains Mono,monospace" font-size="12">DRAM</text>
        <rect x="180" y="185" width="100" height="44" rx="8" fill="#fffcf7" stroke="#3d6b8c" stroke-width="1.5"/>
        <text x="230" y="212" text-anchor="middle" fill="#1a1f2e" font-family="JetBrains Mono,monospace" font-size="11">SRAM</text>
        <rect x="300" y="185" width="100" height="44" rx="8" fill="#fffcf7" stroke="#c4783a" stroke-width="1.5"/>
        <text x="350" y="205" text-anchor="middle" fill="#1a1f2e" font-family="JetBrains Mono,monospace" font-size="11">AXI-Lite</text>
        <text x="350" y="220" text-anchor="middle" fill="#4a5568" font-family="Source Sans 3,sans-serif" font-size="10">bridge → APB</text>

        <rect x="480" y="50" width="160" height="50" rx="8" fill="#fffcf7" stroke="#c4783a" stroke-width="1.5"/>
        <text x="560" y="80" text-anchor="middle" fill="#1a1f2e" font-family="JetBrains Mono,monospace" font-size="12">Camera / DSP</text>
        <rect x="480" y="120" width="340" height="44" rx="8" fill="#c4783a"/>
        <text x="650" y="147" text-anchor="middle" fill="#fffcf7" font-family="Source Sans 3,sans-serif" font-size="14" font-weight="700">AXI-Stream pipeline (no addresses)</text>
        <rect x="660" y="185" width="160" height="44" rx="8" fill="#fffcf7" stroke="#c4783a" stroke-width="1.5"/>
        <text x="740" y="212" text-anchor="middle" fill="#1a1f2e" font-family="JetBrains Mono,monospace" font-size="12">Display DMA</text>

        <rect x="480" y="185" width="150" height="44" rx="8" fill="#fffcf7" stroke="#2f6b4a" stroke-width="1.5"/>
        <text x="555" y="205" text-anchor="middle" fill="#1a1f2e" font-family="JetBrains Mono,monospace" font-size="11">APB island</text>
        <text x="555" y="220" text-anchor="middle" fill="#4a5568" font-family="Source Sans 3,sans-serif" font-size="10">UART · I²C · GPIO</text>
      </svg>
      <figcaption>Fig. Fast path (AXI), config path (APB), streaming path (AXIS) — three jobs, three fabrics.</figcaption>
    </figure>
  </section>

  <!-- 07 WHEN -->
  <section id="when">
    <div class="section-head">
      <span class="section-num">07</span>
      <h2>When to use what</h2>
    </div>
    <p class="lede">Decision shortcuts you can use while architecting a student SoC — or reading a block diagram.</p>

    <div class="decision">
      <div class="row">
        <div class="q">CPU programming UART / timer / GPIO registers</div>
        <div class="a">APB (or AXI-Lite)</div>
      </div>
      <div class="row">
        <div class="q">CPU or DMA moving big buffers to DRAM</div>
        <div class="a">AXI (bursts)</div>
      </div>
      <div class="row">
        <div class="q">Control registers sitting on an AXI interconnect</div>
        <div class="a">AXI-Lite slave</div>
      </div>
      <div class="row">
        <div class="q">Pixels / samples flowing stage → stage</div>
        <div class="a">AXI-Stream</div>
      </div>
      <div class="row">
        <div class="q">Tiny FPGA soft-core, teaching Wishbone IP</div>
        <div class="a">Wishbone / AHB-Lite</div>
      </div>
      <div class="row">
        <div class="q">Many coherent CPU cores sharing caches</div>
        <div class="a">ACE / CHI / TileLink</div>
      </div>
      <div class="row">
        <div class="q">Chip-to-chip high bandwidth</div>
        <div class="a">PCIe (not on-chip bus)</div>
      </div>
    </div>

    <div class="callout ok">
      <strong>Rule of thumb</strong>
      Bandwidth &amp; concurrency → AXI.
      Simplicity &amp; peripherals → APB.
      Dataflow pipelines → AXI-Stream.
      Don’t put a 115200 baud UART on a 128-bit AXI port “because AXI is better.”
    </div>

    <div class="card">
      <h3>Cost vs capability (mental scale)</h3>
      <table class="cmp">
        <thead>
          <tr><th></th><th>Gate cost</th><th>Peak BW</th><th>Outstanding txns</th><th>Best at</th></tr>
        </thead>
        <tbody>
          <tr><td>APB</td><td>Lowest</td><td>Low</td><td>No</td><td>Config</td></tr>
          <tr><td>AHB-Lite</td><td>Low</td><td>Medium</td><td>Limited</td><td>Small systems</td></tr>
          <tr><td>AXI-Lite</td><td>Low–mid</td><td>Medium</td><td>Yes (simple)</td><td>Regs on AXI</td></tr>
          <tr><td>AXI</td><td>Higher</td><td>High</td><td>Yes</td><td>Memory traffic</td></tr>
          <tr><td>AXI-Stream</td><td>Low per link</td><td>High (sustained)</td><td>N/A (flow)</td><td>Pipelines</td></tr>
        </tbody>
      </table>
    </div>
  </section>

  <!-- 08 MODERN -->
  <section id="modern">
    <div class="section-head">
      <span class="section-num">08</span>
      <h2>From “one bus” to interconnects</h2>
    </div>
    <p class="lede">
      Textbook diagrams show a single shared bus. Phone SoCs are networks.
    </p>

    <div class="two">
      <div class="card" style="margin:0">
        <h3>Shared bus</h3>
        <ul>
          <li>One transaction “owns” the wires</li>
          <li>Easy to reason about</li>
          <li>Throughput collapses as masters multiply</li>
        </ul>
      </div>
      <div class="card" style="margin:0">
        <h3>Crossbar</h3>
        <ul>
          <li>Multiple master→slave pairs at once</li>
          <li>Still address-mapped</li>
          <li>Wire/mux cost grows with ports</li>
        </ul>
      </div>
    </div>
    <div class="card">
      <h3>Network-on-Chip (NoC)</h3>
      <p>
        Routers and links, packets with destination IDs, sometimes virtual channels.
        Scales to dozens of agents. Latency and congestion become network problems —
        still “a bus” from the IP author’s point of view (you still see an AXI port),
        but the middle is a fabric.
      </p>
    </div>

    <div class="callout warn">
      <strong>Vocabulary trap</strong>
      People say “the AXI bus” even when they mean “an AXI crossbar interconnect.”
      Protocol (AXI) ≠ topology (shared vs crossbar vs NoC).
    </div>
  </section>

  <!-- 09 QA -->
  <section id="qa">
    <div class="section-head">
      <span class="section-num">09</span>
      <h2>Q&amp;A</h2>
    </div>
    <div class="qa">
      <details>
        <summary>Is AXI-Stream a bus?</summary>
        <p>
          It’s a streaming interface standard. Point-to-point links don’t need a global arbiter.
          The moment many streams share a switch or DMA, you’re back to fabric + scheduling.
        </p>
      </details>
      <details>
        <summary>Why not make everything AXI?</summary>
        <p>
          Silicon and verification cost. A GPIO block does not need burst channels and five handshake lanes.
          Bridges (AXI→APB) exist so cheap slaves can live on an expensive fabric.
        </p>
      </details>
      <details>
        <summary>Where does arbitration live in AXI?</summary>
        <p>
          Inside the interconnect IP (crossbar / NIC), not inside every slave.
          Each master thinks it has a private AXI port; the fabric multiplexes internally.
        </p>
      </details>
      <details>
        <summary>How is this like a processor pipeline?</summary>
        <p>
          Address/data phases can pipeline (AHB). AXI splits channels so request and response
          overlap like multi-issue memory ops. Stalls and backpressure are the same physics
          as pipeline holds — just across IP boundaries.
        </p>
      </details>
      <details>
        <summary>What should a student SoC start with?</summary>
        <p>
          CPU + SRAM on AHB-Lite or AXI-Lite, peripherals on APB, one DMA later on AXI,
          and AXI-Stream only if you have a real dataflow (video/DSP) lab.
        </p>
      </details>
    </div>
  </section>

  <footer>
    Related lectures:
    <a href="../handshaking/index.html">AXI Handshaking</a>
    ·
    <a href="../axistream/index.html">AXI-Stream</a>
    ·
    <a href="../skidBuffer/index.html">Skid Buffer</a>
  </footer>
</main>

<script>
(function () {
  // Scripted requests per cycle: bit0=CPU, bit1=DMA, bit2=GPU
  const pattern = [
    0b001, // CPU
    0b011, // CPU+DMA
    0b111, // all three
    0b110, // DMA+GPU
    0b100, // GPU alone
    0b010, // DMA
    0b111,
    0b001,
    0b000,
    0b110,
  ];

  const names = ["CPU", "DMA", "GPU"];
  let cycle = 0;
  let rrPtr = 0; // next to try in round-robin
  let timer = null;

  const statusEl = document.getElementById("arbStatus");
  const railEl = document.getElementById("busRail");
  const policyEl = document.getElementById("policy");
  const cards = [0, 1, 2].map((i) => document.getElementById("m" + i));

  function requesting(mask) {
    return [0, 1, 2].map((i) => !!(mask & (1 << i)));
  }

  function choose(mask, policy) {
    const req = requesting(mask);
    if (!req.some(Boolean)) return -1;

    if (policy === "priority") {
      for (let i = 0; i < 3; i++) if (req[i]) return i;
    }

    // round-robin: start from rrPtr, wrap
    for (let k = 0; k < 3; k++) {
      const i = (rrPtr + k) % 3;
      if (req[i]) return i;
    }
    return -1;
  }

  function render() {
    const mask = pattern[cycle % pattern.length];
    const policy = policyEl.value;
    const req = requesting(mask);
    const winner = choose(mask, policy);

    cards.forEach((card, i) => {
      card.classList.remove("active", "waiting");
      const p = card.querySelector("p");
      if (!req[i]) {
        p.textContent = "idle";
      } else if (i === winner) {
        card.classList.add("active");
        p.textContent = "REQUEST · GRANTED";
      } else {
        card.classList.add("waiting");
        p.textContent = "REQUEST · waiting";
      }
    });

    if (winner < 0) {
      railEl.innerHTML = '<span class="idle">bus idle</span>';
    } else {
      railEl.innerHTML = '<span class="grant">GRANT → ' + names[winner] +
        "</span> &nbsp;|&nbsp; policy=" + (policy === "priority" ? "fixed priority" : "round-robin");
      if (policy === "rr") rrPtr = (winner + 1) % 3;
    }

    statusEl.textContent = "cycle " + cycle + " · req mask " + mask.toString(2).padStart(3, "0");
  }

  function step() {
    cycle++;
    render();
  }

  function reset() {
    clearInterval(timer);
    timer = null;
    cycle = 0;
    rrPtr = 0;
    render();
  }

  document.getElementById("btnStep").onclick = () => { clearInterval(timer); timer = null; step(); };
  document.getElementById("btnReset").onclick = reset;
  document.getElementById("btnAuto").onclick = () => {
    clearInterval(timer);
    timer = setInterval(step, 850);
  };
  policyEl.onchange = () => { rrPtr = 0; render(); };

  render();
})();
</script>
</body>
</html>


