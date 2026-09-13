## AXI-Stream lecture

[index.html](https://github.com/user-attachments/files/32155558/index.html)
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>AXI-Stream — Streams</title>
  <link rel="stylesheet" href="css/styles.css" />
  <style>
    .sig-table { width: 100%; border-collapse: collapse; font-size: 0.95rem; }
    .sig-table th, .sig-table td {
      border: 1px solid var(--line); padding: 0.55rem 0.7rem; text-align: left; vertical-align: top;
    }
    .sig-table th {
      background: #eef4f8; font-size: 0.78rem; text-transform: uppercase;
      letter-spacing: 0.04em; color: var(--ink-soft);
    }
    .sig-table code {
      font-size: 0.86rem; background: #eef4f8; padding: 0.05rem 0.3rem; border-radius: 4px;
    }
    .packet-strip {
      display: flex; flex-wrap: wrap; gap: 0.4rem; min-height: 2.2rem; align-items: center;
      margin-top: 0.5rem;
    }
    .beat-chip {
      font-family: var(--mono); font-size: 0.72rem; font-weight: 600;
      padding: 0.35rem 0.55rem; border-radius: 6px;
      background: #e8eef6; border: 1px solid #b7c7da; color: var(--teal-deep);
    }
    .beat-chip small { opacity: 0.75; margin-left: 0.25rem; }
    .beat-chip.last { background: #fff4e8; border-color: #d4a017; color: #7a5a00; }
    .beat-chip.idle { background: #f3f6f8; color: var(--ink-soft); font-weight: 500; }
    .box.wire { border-style: dashed; background: #f7fafc; min-height: 140px; }
    .compare {
      display: grid; grid-template-columns: 1fr 1fr; gap: 0.75rem;
    }
    @media (max-width: 700px) { .compare { grid-template-columns: 1fr; } }
    .compare .card h3 {
      font-family: var(--display); font-size: 1.05rem; margin: 0 0 0.4rem;
    }
    .story {
      font-size: 1.05rem; color: var(--ink-soft); max-width: 40rem;
    }
    .next-up {
      border: 1px solid var(--line);
      background: linear-gradient(135deg, #f7fafc 0%, #e8eef6 100%);
      border-radius: var(--radius);
      padding: 1.1rem 1.25rem;
    }
    .next-up h2 {
      font-family: var(--display); font-size: 1.25rem; margin: 0 0 0.4rem;
    }
  </style>
</head>
<body>
  <header class="topbar">
    <div class="topbar-inner">
      <div class="brand">AXI-Stream</div>
      <nav class="nav" aria-label="Sections">
        <a href="#bridge">From where we are</a>
        <a href="#idea">The idea</a>
        <a href="#signals">Signals</a>
        <a href="#fire">When data moves</a>
        <a href="#packets">Packets</a>
        <a href="#simulator">Live walk</a>
        <a href="#scenarios">Scenarios</a>
        <a href="#code">Code</a>
        <a href="#traps">Traps</a>
        <a href="#next">Next</a>
      </nav>
    </div>
  </header>

  <main class="wrap">
    <header class="hero">
      <p class="hero-kicker">After handshaking · skid buffers · pipelines</p>
      <h1>Meet the stream</h1>
      <p class="hero-lead story">
        You already know how two blocks agree to pass data:
        <code>VALID</code> and <code>READY</code>.
        You know why a skid buffer exists when that ready signal is registered.
        Today we name the highway those handshakes ride on —
        <strong>AXI4-Stream</strong> — and learn how a continuous flow of beats
        becomes packets with a single extra flag: <code>TLAST</code>.
      </p>
      <div class="hero-meta">
        <span class="pill">One-way data path</span>
        <span class="pill">Same handshake you know</span>
        <span class="pill">Foundation for the next lecture</span>
      </div>
    </header>

    <!-- BRIDGE -->
    <section id="bridge">
      <div class="section-head">
        <span class="section-num">01</span>
        <h2>From pipelines to a named bus</h2>
      </div>
      <div class="card">
        <p style="margin-top:0;font-size:1.05rem">
          In a processor pipeline, stage&nbsp;N offers a result and stage&nbsp;N+1
          decides whether it can take it. That is already a stream of instructions —
          we just drew it as boxes and arrows.
        </p>
        <p>
          AXI-Stream is the <em>same idea</em>, written as a standard interface so
          video blocks, DSP filters, DMA engines, and your own IP can plug together
          without reinventing the wires every time.
        </p>
        <div class="compare" style="margin-top:1rem">
          <div class="card" style="margin:0;box-shadow:none;background:#f7fafc">
            <h3>What you already know</h3>
            <ul style="margin:0;padding-left:1.1rem;color:var(--ink-soft)">
              <li>VALID / READY handshake</li>
              <li>Hold rule when stalled</li>
              <li>Skid buffer → registered ready without losing a beat</li>
              <li>Pipeline stages passing work forward</li>
            </ul>
          </div>
          <div class="card" style="margin:0;box-shadow:none;background:#eef3f8">
            <h3>What is new today</h3>
            <ul style="margin:0;padding-left:1.1rem;color:var(--ink-soft)">
              <li>The AXI-Stream signal names (<code>T…</code>)</li>
              <li>Beats vs packets</li>
              <li><code>TLAST</code> as “end of this group”</li>
              <li><code>TKEEP</code> when the last beat is only partly full</li>
            </ul>
          </div>
        </div>
        <div class="callout" style="margin-bottom:0;margin-top:1rem">
          <strong>Not today:</strong> full AXI with addresses, reads, writes, and
          response channels. That is a different animal. A stream has
          <em>no address</em> — it is just cargo moving one direction.
        </div>
      </div>
    </section>

    <!-- IDEA -->
    <section id="idea">
      <div class="section-head">
        <span class="section-num">02</span>
        <h2>Picture a conveyor</h2>
      </div>
      <div class="grid-2">
        <div class="card">
          <p style="margin-top:0">
            The <strong>master</strong> places boxes on the belt.
            The <strong>slave</strong> takes boxes off the belt.
          </p>
          <ul>
            <li><code>TVALID</code> — “there is a box here”</li>
            <li><code>TREADY</code> — “I can take a box now”</li>
            <li><code>TDATA</code> — what is inside the box</li>
            <li><code>TLAST</code> — “this box closes the shipment”</li>
          </ul>
          <p style="margin-bottom:0">
            If the worker downstream is busy, they lower ready.
            The box stays put — same hold rule you learned with handshakes.
            If ready is registered and you still need full throughput, that is
            exactly where a <strong>skid buffer</strong> belongs on a stream.
          </p>
        </div>
        <div class="card">
          <div class="diagram" aria-hidden="true">
            <svg viewBox="0 0 420 190" width="400" height="180">
              <rect x="16" y="55" width="110" height="78" rx="8" fill="#fff" stroke="#7aa0b8" stroke-width="2"/>
              <text x="71" y="92" text-anchor="middle" font-family="Source Sans 3" font-size="15" fill="#13212e">Master</text>
              <text x="71" y="112" text-anchor="middle" font-family="JetBrains Mono" font-size="10" fill="#3a4a5a">source</text>

              <rect x="155" y="78" width="28" height="22" rx="3" fill="#1a4f8a"/>
              <rect x="195" y="78" width="28" height="22" rx="3" fill="#1a4f8a"/>
              <rect x="235" y="78" width="36" height="22" rx="3" fill="#d4a017"/>
              <text x="253" y="93" text-anchor="middle" font-size="8" font-family="JetBrains Mono" fill="#fff">LAST</text>
              <line x1="145" y1="120" x2="280" y2="120" stroke="#c5d0db" stroke-width="6" stroke-linecap="round"/>

              <rect x="294" y="55" width="110" height="78" rx="8" fill="#fff" stroke="#2a7a9b" stroke-width="2"/>
              <text x="349" y="92" text-anchor="middle" font-family="Source Sans 3" font-size="15" fill="#13212e">Slave</text>
              <text x="349" y="112" text-anchor="middle" font-family="JetBrains Mono" font-size="10" fill="#3a4a5a">sink</text>

              <path d="M128 75 H150" stroke="#1a4f8a" stroke-width="2"/>
              <path d="M271 75 H292" stroke="#1a4f8a" stroke-width="2"/>
              <path d="M292 115 H128" stroke="#c24b3a" stroke-width="2" marker-end="url(#ar)"/>
              <text x="210" y="50" text-anchor="middle" font-family="JetBrains Mono" font-size="11" fill="#1a4f8a">TVALID · TDATA · TLAST →</text>
              <text x="210" y="148" text-anchor="middle" font-family="JetBrains Mono" font-size="11" fill="#c24b3a">← TREADY</text>
              <text x="210" y="172" text-anchor="middle" font-family="Source Sans 3" font-size="12" fill="#3a4a5a">one shipment = several boxes, sealed by LAST</text>
              <defs>
                <marker id="ar" markerWidth="8" markerHeight="8" refX="6" refY="3" orient="auto">
                  <path d="M0,0 L6,3 L0,6 Z" fill="#c24b3a"/>
                </marker>
              </defs>
            </svg>
          </div>
        </div>
      </div>
    </section>

    <!-- SIGNALS -->
    <section id="signals">
      <div class="section-head">
        <span class="section-num">03</span>
        <h2>The wires — start with four</h2>
      </div>
      <div class="card">
        <p style="margin-top:0">
          The leading <code>T</code> just means “transfer.” Read them out loud once —
          they will stick.
        </p>
        <table class="sig-table">
          <thead>
            <tr><th>Signal</th><th>Who drives it</th><th>Meaning</th></tr>
          </thead>
          <tbody>
            <tr>
              <td><code>TVALID</code></td>
              <td>Master</td>
              <td>I am offering a beat.</td>
            </tr>
            <tr>
              <td><code>TREADY</code></td>
              <td>Slave</td>
              <td>I can accept a beat.</td>
            </tr>
            <tr>
              <td><code>TDATA</code></td>
              <td>Master</td>
              <td>The payload (often 32 or 64 bits).</td>
            </tr>
            <tr>
              <td><code>TLAST</code></td>
              <td>Master</td>
              <td>This beat ends the current packet.</td>
            </tr>
          </tbody>
        </table>
        <p style="margin:1rem 0 0.5rem">Useful extras — we will touch them, not live in them yet:</p>
        <table class="sig-table">
          <thead>
            <tr><th>Signal</th><th>Meaning in one line</th></tr>
          </thead>
          <tbody>
            <tr><td><code>TKEEP</code></td><td>Which bytes inside <code>TDATA</code> are real (partial last beat).</td></tr>
            <tr><td><code>TUSER</code></td><td>Sideband flags (for example start-of-frame in video).</td></tr>
            <tr><td><code>TID</code> / <code>TDEST</code></td><td>Stream ID / where to route — later, when we build switches.</td></tr>
            <tr><td><code>ACLK</code> / <code>ARESETn</code></td><td>Clock and active-low reset (AXI naming).</td></tr>
          </tbody>
        </table>
      </div>
    </section>

    <!-- FIRE -->
    <section id="fire">
      <div class="section-head">
        <span class="section-num">04</span>
        <h2>When does data actually move?</h2>
      </div>
      <div class="card">
        <p style="margin-top:0;font-size:1.08rem">
          On a rising clock edge, a beat transfers only if both sides agree:
        </p>
        <div class="code-block">
          <div class="code-head"><span>one line you will write forever</span></div>
          <pre><span class="c-kw">wire</span> fire = tvalid &amp;&amp; tready;</pre>
        </div>
        <p>
          That is the same handshake you already practiced — AXI-Stream just
          prefixes the names with <code>T</code>.
        </p>
        <div class="callout warn">
          <strong>Hold rule (unchanged):</strong>
          if <code>TVALID=1</code> and <code>TREADY=0</code>, the master must keep
          <code>TVALID</code>, <code>TDATA</code>, <code>TKEEP</code>, and
          <code>TLAST</code> stable until the slave accepts.
          Change them early and you invent a ghost beat.
        </div>
        <table class="rules" style="margin-top:1rem">
          <thead>
            <tr><th>TVALID</th><th>TREADY</th><th>What is happening</th></tr>
          </thead>
          <tbody>
            <tr><td>1</td><td>1</td><td><strong>Fire</strong> — beat transfers this cycle</td></tr>
            <tr><td>1</td><td>0</td><td><strong>Backpressure</strong> — slave says wait; master holds</td></tr>
            <tr><td>0</td><td>1</td><td><strong>Bubble</strong> — master has nothing; slave is waiting</td></tr>
            <tr><td>0</td><td>0</td><td>Both quiet — also fine</td></tr>
          </tbody>
        </table>
      </div>
    </section>

    <!-- PACKETS -->
    <section id="packets">
      <div class="section-head">
        <span class="section-num">05</span>
        <h2>Beats and packets</h2>
      </div>
      <div class="card">
        <div class="analogy">
          <svg class="analogy-art" viewBox="0 0 120 120" aria-hidden="true">
            <rect x="10" y="28" width="100" height="64" rx="8" fill="#fff" stroke="#1a4f8a" stroke-width="2"/>
            <text x="60" y="48" text-anchor="middle" font-size="12" font-family="Source Sans 3" fill="#0f355f">one packet</text>
            <rect x="20" y="58" width="22" height="20" rx="3" fill="#1a4f8a"/>
            <rect x="46" y="58" width="22" height="20" rx="3" fill="#1a4f8a"/>
            <rect x="72" y="58" width="28" height="20" rx="3" fill="#d4a017"/>
            <text x="86" y="72" text-anchor="middle" font-size="8" font-family="JetBrains Mono" fill="#fff">LAST</text>
          </svg>
          <div>
            <p style="margin-top:0">
              A <strong>beat</strong> is one successful handshake — one word of
              <code>TDATA</code> crossing the interface.
            </p>
            <p>
              A <strong>packet</strong> is a run of beats that ends when a beat
              with <code>TLAST=1</code> is accepted. One beat can be a whole
              packet if that beat carries <code>TLAST</code>.
            </p>
            <p style="margin-bottom:0">
              Think of a video line, an Ethernet frame, or “this many samples
              belong together.” <code>TLAST</code> is how the stream says
              <em>group boundary</em> without sending an address.
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- SIMULATOR -->
    <section id="simulator">
      <div class="section-head">
        <span class="section-num">06</span>
        <h2>Watch a stream move</h2>
      </div>
      <div class="card">
        <p style="margin-top:0">
          Step or play. Green edge = fire. Red edge = valid stuck waiting on ready.
          The chip row below shows beats the slave has actually accepted.
        </p>
        <div class="tabs" role="tablist">
          <button type="button" class="tab active" data-scenario="continuous">Steady flow</button>
          <button type="button" class="tab" data-scenario="backpressure">Backpressure</button>
          <button type="button" class="tab" data-scenario="packet">Two packets</button>
          <button type="button" class="tab" data-scenario="tkeep">Partial KEEP</button>
          <button type="button" class="tab" data-scenario="bubbles">Bubbles</button>
        </div>
        <h3 id="scenarioTitle" style="font-family:var(--display);margin:.2rem 0 .7rem;">Steady flow</h3>

        <div class="sim-controls">
          <button type="button" class="btn" id="btnPrev">← Prev</button>
          <button type="button" class="btn primary" id="btnPlay">Play</button>
          <button type="button" class="btn" id="btnNext">Next →</button>
          <button type="button" class="btn danger" id="btnReset">Reset</button>
        </div>

        <div class="sim-shell">
          <div>
            <div class="cycle-label" id="cycleLabel">Cycle 0</div>
            <div class="wire-board">
              <div class="pipeline">
                <div class="box producer" id="boxMst">
                  <h4>Master</h4>
                  <div class="signal"><span class="name">TVALID</span><span class="val" id="v_tv">0</span></div>
                  <div class="signal"><span class="name">TDATA</span><span class="val" id="v_td">0x00000000</span></div>
                  <div class="signal"><span class="name">TKEEP</span><span class="val" id="v_tk">0xF</span></div>
                  <div class="signal"><span class="name">TLAST</span><span class="val" id="v_tl">0</span></div>
                </div>
                <div class="arrow-col">⇄</div>
                <div class="box wire" id="boxWire">
                  <h4>This cycle</h4>
                  <div class="signal"><span class="name">FIRE</span><span class="val" id="v_fire">no</span></div>
                  <div class="signal"><span class="name">beats</span><span class="val" id="v_beats">0</span></div>
                  <div class="signal"><span class="name">packets</span><span class="val" id="v_pkts">0</span></div>
                  <div class="signal"><span class="name">need</span><span class="val">V &amp;&amp; R</span></div>
                </div>
                <div class="arrow-col">⇄</div>
                <div class="box consumer" id="boxSlv">
                  <h4>Slave</h4>
                  <div class="signal"><span class="name">TREADY</span><span class="val" id="v_tr">1</span></div>
                  <div class="signal"><span class="name">takes data</span><span class="val">on fire</span></div>
                  <div class="signal"><span class="name">closes pkt</span><span class="val">on LAST</span></div>
                </div>
              </div>
            </div>
            <div>
              <strong style="font-size:0.85rem;color:var(--ink-soft)">Accepted so far</strong>
              <div class="packet-strip" id="packetStrip"></div>
            </div>
            <div class="explain" id="explainBox" style="margin-top:0.75rem">Loading…</div>
          </div>
          <div>
            <div class="code-head" style="border:1px solid var(--line);border-bottom:0;border-radius:8px 8px 0 0;background:#0c1620">Cycle history</div>
            <div class="wave" id="waveBox" style="border-radius:0 0 8px 8px"></div>
          </div>
        </div>
      </div>
    </section>

    <!-- SCENARIOS -->
    <section id="scenarios">
      <div class="section-head">
        <span class="section-num">07</span>
        <h2>Scenarios worth locking in</h2>
      </div>

      <div class="tabs">
        <button type="button" class="tab active" data-panel="panel-cont">Steady</button>
        <button type="button" class="tab" data-panel="panel-bp">Stall</button>
        <button type="button" class="tab" data-panel="panel-pkt">Packets</button>
        <button type="button" class="tab" data-panel="panel-keep">KEEP</button>
        <button type="button" class="tab" data-panel="panel-idle">Bubbles</button>
      </div>

      <div class="scenario-panel active card" id="panel-cont">
        <h3 style="font-family:var(--display);margin-top:0">Steady flow</h3>
        <p>
          Slave stays ready. Every offered beat fires the same cycle.
          That is a full-rate stream — one beat per clock — the dream case
          for video and DSP pipelines.
        </p>
        <div class="code-block">
          <div class="code-head"><span>progress only when both agree</span></div>
          <pre><span class="c-kw">wire</span> fire = s_axis_tvalid &amp;&amp; s_axis_tready;
<span class="c-com">// sample tdata / tlast only when fire is true</span></pre>
        </div>
      </div>

      <div class="scenario-panel card" id="panel-bp">
        <h3 style="font-family:var(--display);margin-top:0">Backpressure</h3>
        <p>
          Downstream is full (FIFO nearly full, slow sink). Slave drops
          <code>TREADY</code>. Master freezes the offer. Nothing is dropped —
          the beat simply waits, exactly like a stalled pipeline stage.
        </p>
        <div class="code-block">
          <div class="code-head"><span>master advances only on fire</span></div>
          <pre><span class="c-kw">else if</span> (active &amp;&amp; fire) <span class="c-kw">begin</span>
  <span class="c-com">// next beat or end of packet</span>
<span class="c-kw">end</span>
<span class="c-com">// if tvalid && !tready: do nothing → hold rule satisfied</span></pre>
        </div>
        <div class="callout">
          <strong>Link to last lecture:</strong> if you register <code>TREADY</code>
          for timing, the one beat that still slips in needs a parking spot —
          a skid buffer on the stream.
        </div>
      </div>

      <div class="scenario-panel card" id="panel-pkt">
        <h3 style="font-family:var(--display);margin-top:0">Packets and TLAST</h3>
        <p>
          The slave counts beats every fire. When the accepted beat has
          <code>TLAST</code>, it also counts a completed packet — time to close
          a buffer, raise an interrupt, or start the next line of pixels.
        </p>
        <div class="code-block">
          <div class="code-head"><span>closing a packet</span></div>
          <pre><span class="c-kw">if</span> (fire) <span class="c-kw">begin</span>
  beat_count &lt;= beat_count + 1;
  <span class="c-kw">if</span> (s_axis_tlast)
    packet_count &lt;= packet_count + 1;
<span class="c-kw">end</span></pre>
        </div>
      </div>

      <div class="scenario-panel card" id="panel-keep">
        <h3 style="font-family:var(--display);margin-top:0">Partial last beat — TKEEP</h3>
        <p>
          Bus is 4 bytes wide, packet is 6 bytes: first beat keeps all four,
          last beat keeps only two. Bytes with <code>TKEEP=0</code> are padding —
          the slave must ignore them.
        </p>
        <div class="code-block">
          <div class="code-head"><span>last beat of a short packet</span></div>
          <pre>tdata = 32'h0000_1122;
tkeep = 4'b0011;   <span class="c-com">// only low two bytes count</span>
tlast = 1'b1;</pre>
        </div>
      </div>

      <div class="scenario-panel card" id="panel-idle">
        <h3 style="font-family:var(--display);margin-top:0">Bubbles are not stalls</h3>
        <p>
          <code>TVALID=0</code> while <code>TREADY=1</code> means the master
          paused. That is a bubble in the stream — legal, common, and different
          from backpressure (<code>TREADY=0</code>).
        </p>
      </div>
    </section>

    <!-- CODE -->
    <section id="code">
      <div class="section-head">
        <span class="section-num">08</span>
        <h2>Reference code in this folder</h2>
      </div>
      <div class="card">
        <p style="margin-top:0">
          Open these beside the projector when you want to see the hold rule in RTL:
        </p>
        <ul>
          <li><code>sv/axis_master_teaching.sv</code> — sends a packet; advances only on fire</li>
          <li><code>sv/axis_slave_teaching.sv</code> — accepts with a ready gate; counts beats and packets</li>
          <li><code>sv/tb_axis_demo.sv</code> — steady flow, then a mid-packet stall</li>
          <li><code>sv/axis_rules_excerpt.sv</code> — the hold rule written as assertions</li>
        </ul>
        <div class="code-block">
          <div class="code-head"><span>shape of a correct master</span></div>
          <pre><span class="c-kw">wire</span> fire = m_axis_tvalid &amp;&amp; m_axis_tready;

<span class="c-kw">always_ff</span> @(posedge aclk <span class="c-kw">or negedge</span> aresetn) <span class="c-kw">begin</span>
  <span class="c-kw">if</span> (!aresetn)
    m_axis_tvalid &lt;= 1'b0;
  <span class="c-kw">else if</span> (!active &amp;&amp; i_start)
    <span class="c-com">/* raise tvalid, load first beat, set tlast if length==1 */</span>
  <span class="c-kw">else if</span> (active &amp;&amp; fire)
    <span class="c-com">/* last? clear valid : offer next beat */</span>
  <span class="c-com">/* else stalled: outputs stay as they are */</span>
<span class="c-kw">end</span></pre>
        </div>
      </div>
    </section>

    <!-- TRAPS -->
    <section id="traps">
      <div class="section-head">
        <span class="section-num">09</span>
        <h2>Traps that show up in lab</h2>
      </div>
      <div class="card">
        <table class="rules">
          <thead><tr><th>Trap</th><th>What goes wrong</th><th>Habit that saves you</th></tr></thead>
          <tbody>
            <tr>
              <td>Change <code>TDATA</code> while valid and not ready</td>
              <td>Wrong beat gets accepted later</td>
              <td>Update stream outputs only when <code>!tvalid || tready</code></td>
            </tr>
            <tr>
              <td>Forget <code>TLAST</code></td>
              <td>Packet never ends; sink waits forever</td>
              <td>Plan the last beat first, then fill the middle</td>
            </tr>
            <tr>
              <td>Assume ready is always 1</td>
              <td>Works until a real FIFO fills</td>
              <td>Always qualify with <code>fire</code></td>
            </tr>
            <tr>
              <td>Treat AXIS like full AXI</td>
              <td>Hunting for addresses that do not exist</td>
              <td>Stream = one-way cargo; no address phase</td>
            </tr>
          </tbody>
        </table>
      </div>
    </section>

    <!-- NEXT -->
    <section id="next">
      <div class="section-head">
        <span class="section-num">10</span>
        <h2>Where this goes next</h2>
      </div>
      <div class="next-up">
        <h2>We have the stream. Next we build on it.</h2>
        <p style="margin:0 0 0.75rem;color:var(--ink-soft);font-size:1.05rem">
          Today’s goal was the interface itself: names, fire, packets, keep,
          and the link back to handshakes and skid buffers.
          In the next lecture we start composing blocks on this stream —
          registering paths, buffering, and connecting real producers and consumers.
        </p>
        <p style="margin:0;color:var(--ink-soft)">
          Carry forward one sentence:
          <strong style="color:var(--ink)"><code>fire = tvalid &amp;&amp; tready</code>,
          and never move on until it fires.</strong>
        </p>
      </div>
    </section>

    <footer class="footer">
      <p>
        AXI4-Stream fundamentals · builds on VALID/READY handshaking and skid buffers.
        Companion code lives in <code>sv/</code>.
      </p>
    </footer>
  </main>

  <script src="js/lecture.js"></script>
</body>
</html>
