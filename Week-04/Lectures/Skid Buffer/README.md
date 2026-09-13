## Skid Buffer lecture

[index.html](https://github.com/user-attachments/files/32155590/index.html)

=========================================================


<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Skid Buffer</title>
  <link rel="stylesheet" href="css/styles.css" />
  <style>
    .compare {
      display: grid; grid-template-columns: 1fr 1fr; gap: 0.75rem;
    }
    @media (max-width: 700px) { .compare { grid-template-columns: 1fr; } }
    .compare .card h3 {
      font-family: var(--display); font-size: 1.05rem; margin: 0 0 0.4rem;
    }
    .story {
      font-size: 1.05rem; color: var(--ink-soft); max-width: 42rem;
    }
    .next-up {
      border: 1px solid var(--line);
      background: linear-gradient(135deg, #f7fafc 0%, #eef7f6 100%);
      border-radius: var(--radius);
      padding: 1.1rem 1.25rem;
    }
    .next-up h2 {
      font-family: var(--display); font-size: 1.25rem; margin: 0 0 0.4rem;
    }
    .key-line {
      font-family: var(--mono);
      font-size: 1.15rem;
      font-weight: 600;
      color: var(--teal-deep);
      background: #eef7f6;
      border: 1px solid var(--line);
      border-radius: 8px;
      padding: 0.85rem 1rem;
      text-align: center;
      margin: 0.75rem 0;
    }
  </style>
</head>
<body>
  <header class="topbar">
    <div class="topbar-inner">
      <div class="brand">Skid Buffer</div>
      <nav class="nav" aria-label="Sections">
        <a href="#problem">The problem</a>
        <a href="#handshake">Handshake</a>
        <a href="#idea">The idea</a>
        <a href="#simulator">Live walk</a>
        <a href="#scenarios">Scenarios</a>
        <a href="#code">Code</a>
        <a href="#options">Options</a>
        <a href="#rules">Rules</a>
        <a href="#takeaway">Takeaway</a>
      </nav>
    </div>
  </header>

  <main class="wrap">
    <header class="hero">
      <p class="hero-kicker">Pipelines · handshakes · timing</p>
      <h1>The skid buffer</h1>
      <p class="hero-lead story">
        In a pipeline, when a later stage is busy, earlier stages must stop —
        or work gets lost. If that “stop” signal is built from pure combinational
        logic, it can kill your clock frequency. Register the stall instead, and
        one extra beat is already in flight. The
        <strong>skid buffer</strong> is the one-slot parking spot that catches it.
      </p>
      <div class="hero-meta">
        <span class="pill">Registered stall</span>
        <span class="pill">No data lost</span>
        <span class="pill">One memorized line</span>
      </div>
    </header>

    <!-- PROBLEM -->
    <section id="problem">
      <div class="section-head">
        <span class="section-num">01</span>
        <h2>The stall that travels too far</h2>
      </div>
      <div class="card">
        <p style="margin-top:0;font-size:1.05rem">
          Picture a processor pipe: Prefetch → Decode → Operands → Execute.
          Execute hits a long divide. It needs everyone behind it to wait.
        </p>
        <p>
          A common first attempt is a combinational stall chain — each stage
          ORs its busy flag into the stall going upstream:
        </p>
        <div class="code-block">
          <div class="code-head"><span>combinational stall ripple</span></div>
          <pre><span class="c-kw">always_comb</span> <span class="c-kw">begin</span>
  div_stall = div_busy;
  op_stall  = div_stall | mem_busy | cpu_halt;
  dcd_stall = op_stall  | pipeline_hazard;
  pf_stall  = dcd_stall; <span class="c-com">// stall races all the way to the front</span>
<span class="c-kw">end</span></pre>
        </div>
        <div class="callout warn">
          <strong>Timing pain:</strong> every stage adds gate delay on the same net.
          By the time stall reaches prefetch, there may be almost no slack before
          the next clock. Your Fmax collapses.
        </div>
        <div class="compare" style="margin-top:1rem">
          <div class="card" style="margin:0;box-shadow:none;background:#fff4f2">
            <h3>Register the stall?</h3>
            <p style="margin:0;color:var(--ink-soft)">
              Nice for timing — the stop signal is a flip-flop output.
              Bad news: the previous stage does not hear the stop until
              <em>one cycle late</em>. It already launched another beat.
            </p>
          </div>
          <div class="card" style="margin:0;box-shadow:none;background:#eef7f6">
            <h3>So where does that beat go?</h3>
            <p style="margin:0;color:var(--ink-soft)">
              It needs a temporary parking spot, or it vanishes.
              That parking spot is the skid buffer — named for the way the
              stall “skids” one cycle before the producer finally stops.
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- HANDSHAKE -->
    <section id="handshake">
      <div class="section-head">
        <span class="section-num">02</span>
        <h2>VALID / READY — quick refresh</h2>
      </div>
      <div class="grid-2">
        <div class="card">
          <p style="margin-top:0">
            We pass data with the same handshake used all over modern pipelines
            and AXI-style interfaces:
          </p>
          <ul>
            <li><code>VALID</code> — “I am offering a beat”</li>
            <li><code>READY</code> — “I can take a beat”</li>
          </ul>
          <p>
            Transfer (fire) on a rising clock when both are 1:
            <code>fire = valid &amp;&amp; ready</code>.
          </p>
          <div class="callout" style="margin-bottom:0">
            <strong>Hold rule:</strong> if valid is high and ready is low, keep
            valid and data stable until ready rises. No silent changes. No ghosts.
          </div>
        </div>
        <div class="card">
          <div class="diagram" aria-hidden="true">
            <svg viewBox="0 0 420 170" width="400" height="160">
              <rect x="20" y="45" width="110" height="80" rx="8" fill="#fff" stroke="#7aa0b8" stroke-width="2"/>
              <text x="75" y="90" text-anchor="middle" font-family="Source Sans 3" font-size="14">Producer</text>
              <rect x="290" y="45" width="110" height="80" rx="8" fill="#fff" stroke="#1f9d8a" stroke-width="2"/>
              <text x="345" y="90" text-anchor="middle" font-family="Source Sans 3" font-size="14">Consumer</text>
              <path d="M140 65 H280" stroke="#0d6e6e" stroke-width="2.5" marker-end="url(#a1)"/>
              <path d="M280 105 H140" stroke="#c24b3a" stroke-width="2.5" marker-end="url(#a2)"/>
              <text x="210" y="52" text-anchor="middle" font-family="JetBrains Mono" font-size="11" fill="#0d6e6e">VALID + DATA →</text>
              <text x="210" y="128" text-anchor="middle" font-family="JetBrains Mono" font-size="11" fill="#c24b3a">← READY</text>
              <defs>
                <marker id="a1" markerWidth="8" markerHeight="8" refX="6" refY="3" orient="auto"><path d="M0,0 L6,3 L0,6 Z" fill="#0d6e6e"/></marker>
                <marker id="a2" markerWidth="8" markerHeight="8" refX="6" refY="3" orient="auto"><path d="M0,0 L6,3 L0,6 Z" fill="#c24b3a"/></marker>
              </defs>
            </svg>
          </div>
        </div>
      </div>
    </section>

    <!-- IDEA -->
    <section id="idea">
      <div class="section-head">
        <span class="section-num">03</span>
        <h2>One parking spot between stages</h2>
      </div>
      <div class="card">
        <div class="analogy">
          <svg class="analogy-art" viewBox="0 0 120 120" aria-hidden="true">
            <rect x="8" y="70" width="104" height="18" rx="4" fill="#c5d0db"/>
            <rect x="70" y="40" width="36" height="48" rx="4" fill="#fff" stroke="#b8841a" stroke-width="2"/>
            <text x="88" y="68" text-anchor="middle" font-size="9" font-family="Source Sans 3" fill="#b8841a">park</text>
            <rect x="20" y="55" width="34" height="20" rx="3" fill="#0d6e6e"/>
            <circle cx="28" cy="78" r="5" fill="#13212e"/>
            <circle cx="46" cy="78" r="5" fill="#13212e"/>
            <path d="M55 40 L70 40" stroke="#c24b3a" stroke-width="2" stroke-dasharray="3 2"/>
            <text x="60" y="28" text-anchor="middle" font-size="10" font-family="Source Sans 3" fill="#c24b3a">gate closes</text>
          </svg>
          <div>
            <p style="margin-top:0">
              Data is a car. The consumer is a gate. If the gate closes late
              (registered stall), the car already in the intersection needs a
              place to sit. The skid is that single space:
              <code>r_valid</code> / <code>r_data</code>.
            </p>
            <p style="margin-bottom:0">
              When the spot is empty, the buffer looks like a wire.
              When the spot is full, upstream must wait.
            </p>
          </div>
        </div>
      </div>

      <div class="card" style="margin-top:.85rem">
        <div class="key-line">o_ready = !r_valid</div>
        <p style="margin:0;text-align:center;color:var(--ink-soft)">
          Parking spot full → not ready for new input.
          That one flip-flop <em>is</em> your registered upstream stall.
        </p>
        <div class="diagram" style="margin-top:1rem">
          <svg viewBox="0 0 720 200" width="700" height="190">
            <rect x="20" y="60" width="120" height="85" rx="8" fill="#fff" stroke="#7aa0b8" stroke-width="2"/>
            <text x="80" y="105" text-anchor="middle" font-family="Source Sans 3" font-size="13">Upstream</text>
            <text x="80" y="123" text-anchor="middle" font-family="JetBrains Mono" font-size="10" fill="#3a4a5a">i_valid / i_data</text>

            <rect x="210" y="35" width="300" height="135" rx="10" fill="#fffdf5" stroke="#b8841a" stroke-width="2"/>
            <text x="360" y="58" text-anchor="middle" font-family="Fraunces" font-size="16" fill="#084848">Skid Buffer</text>
            <rect x="240" y="78" width="100" height="65" rx="6" fill="#fff" stroke="#d4a017" stroke-width="2"/>
            <text x="290" y="105" text-anchor="middle" font-size="12" font-family="Source Sans 3">r_valid</text>
            <text x="290" y="123" text-anchor="middle" font-size="11" font-family="JetBrains Mono" fill="#b8841a">r_data</text>
            <text x="430" y="105" text-anchor="middle" font-size="12" font-family="JetBrains Mono" fill="#0d6e6e">mux</text>
            <text x="430" y="123" text-anchor="middle" font-size="11" font-family="Source Sans 3" fill="#3a4a5a">→ output</text>

            <rect x="580" y="60" width="120" height="85" rx="8" fill="#fff" stroke="#1f9d8a" stroke-width="2"/>
            <text x="640" y="105" text-anchor="middle" font-family="Source Sans 3" font-size="13">Downstream</text>
            <text x="640" y="123" text-anchor="middle" font-family="JetBrains Mono" font-size="10" fill="#3a4a5a">o_valid / o_data</text>

            <path d="M140 85 H210" stroke="#0d6e6e" stroke-width="2"/>
            <path d="M510 85 H580" stroke="#0d6e6e" stroke-width="2"/>
            <path d="M580 125 H510" stroke="#c24b3a" stroke-width="2"/>
            <path d="M210 125 H140" stroke="#c24b3a" stroke-width="2"/>
            <text x="175" y="78" font-size="10" font-family="JetBrains Mono" fill="#0d6e6e">in</text>
            <text x="165" y="145" font-size="10" font-family="JetBrains Mono" fill="#c24b3a">o_ready</text>
            <text x="540" y="78" font-size="10" font-family="JetBrains Mono" fill="#0d6e6e">out</text>
            <text x="530" y="145" font-size="10" font-family="JetBrains Mono" fill="#c24b3a">i_ready</text>
          </svg>
        </div>
      </div>
    </section>

    <!-- SIMULATOR -->
    <section id="simulator">
      <div class="section-head">
        <span class="section-num">04</span>
        <h2>Watch it cycle by cycle</h2>
      </div>
      <div class="card">
        <p style="margin-top:0">
          Model with combinational outputs (<code>OPT_OUTREG=0</code>) — the clearest
          view of pass-through vs park. Green edge = flowing. Red edge = stalled.
        </p>
        <div class="tabs" role="tablist">
          <button type="button" class="tab active" data-scenario="passthrough">Pass-through</button>
          <button type="button" class="tab" data-scenario="stall_capture">Stall &amp; capture</button>
          <button type="button" class="tab" data-scenario="drain">Drain &amp; recover</button>
          <button type="button" class="tab" data-scenario="backpressure">Why “skid”</button>
        </div>
        <h3 id="scenarioTitle" style="font-family:var(--display);margin:.2rem 0 .7rem;">Pass-through</h3>

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
                <div class="box producer" id="boxProd">
                  <h4>Upstream</h4>
                  <div class="signal"><span class="name">i_valid</span><span class="val" id="v_iv">0</span></div>
                  <div class="signal"><span class="name">i_data</span><span class="val" id="v_id">0x00</span></div>
                  <div class="signal"><span class="name">sees o_ready</span><span class="val" id="v_or">1</span></div>
                </div>
                <div class="arrow-col">→</div>
                <div class="box skid" id="boxSkid">
                  <h4>Skid slot</h4>
                  <div class="signal"><span class="name">r_valid</span><span class="val" id="v_rv">0</span></div>
                  <div class="signal"><span class="name">r_data</span><span class="val" id="v_rd">0x00</span></div>
                  <div class="signal"><span class="name">rule</span><span class="val">ready=!r_valid</span></div>
                </div>
                <div class="arrow-col">→</div>
                <div class="box consumer" id="boxCons">
                  <h4>Downstream</h4>
                  <div class="signal"><span class="name">o_valid</span><span class="val" id="v_ov">0</span></div>
                  <div class="signal"><span class="name">o_data</span><span class="val" id="v_od">0x00</span></div>
                  <div class="signal"><span class="name">i_ready</span><span class="val" id="v_ir">1</span></div>
                </div>
              </div>
            </div>
            <div class="explain" id="explainBox">Loading…</div>
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
        <span class="section-num">05</span>
        <h2>Scenarios worth locking in</h2>
      </div>

      <div class="tabs">
        <button type="button" class="tab active" data-panel="panel-pass">Pass-through</button>
        <button type="button" class="tab" data-panel="panel-copy">Capture</button>
        <button type="button" class="tab" data-panel="panel-active">Skid full</button>
        <button type="button" class="tab" data-panel="panel-drain">Drain</button>
        <button type="button" class="tab" data-panel="panel-outreg">Reg outputs</button>
        <button type="button" class="tab" data-panel="panel-lowpower">Low power</button>
      </div>

      <div class="scenario-panel active card" id="panel-pass">
        <h3 style="font-family:var(--display);margin-top:0">Pass-through — empty parking lot</h3>
        <p>
          Consumer is ready, skid is empty. The buffer behaves like a wire:
          input valid and data show up on the output the same cycle.
        </p>
        <ul class="steps">
          <li><code>r_valid = 0</code> → <code>o_ready = 1</code></li>
          <li><code>o_valid = i_valid</code></li>
          <li><code>o_data = i_data</code></li>
        </ul>
        <div class="code-block">
          <div class="code-head"><span>combinational output path</span></div>
          <pre><span class="c-kw">always_comb</span> <span class="c-kw">begin</span>
  o_valid = i_valid || r_valid;   <span class="c-com">// here r_valid==0</span>
  <span class="c-kw">if</span> (r_valid) o_data = r_data;
  <span class="c-kw">else</span>         o_data = i_data;   <span class="c-com">// pass-through</span>
<span class="c-kw">end</span></pre>
        </div>
      </div>

      <div class="scenario-panel card" id="panel-copy">
        <h3 style="font-family:var(--display);margin-top:0">Capture — gate closes while a beat is offered</h3>
        <p>
          Downstream is not ready, but the skid is still empty so
          <code>o_ready</code> is still 1. The beat is shown on the output
          <em>and</em> copied into the parking spot on this clock.
        </p>
        <ul class="steps">
          <li>Condition: <code>(i_valid &amp;&amp; o_ready) &amp;&amp; (o_valid &amp;&amp; !i_ready)</code></li>
          <li>Action: <code>r_valid &lt;= 1</code>, park <code>i_data</code> in <code>r_data</code></li>
          <li>Next cycle: <code>o_ready</code> falls — upstream must hold</li>
        </ul>
        <div class="code-block">
          <div class="code-head"><span>fill the parking spot</span></div>
          <pre><span class="c-kw">always_ff</span> @(posedge i_clk) <span class="c-kw">begin</span>
  <span class="c-kw">if</span> (i_reset)
    r_valid &lt;= 1'b0;
  <span class="c-kw">else if</span> ((i_valid &amp;&amp; o_ready) &amp;&amp; (o_valid &amp;&amp; !i_ready))
    r_valid &lt;= 1'b1;
  <span class="c-kw">else if</span> (i_ready)
    r_valid &lt;= 1'b0;
<span class="c-kw">end</span></pre>
        </div>
      </div>

      <div class="scenario-panel card" id="panel-active">
        <h3 style="font-family:var(--display);margin-top:0">Skid full — upstream finally stops</h3>
        <p>
          After capture, <code>r_valid=1</code>, so <code>o_ready=0</code>.
          The producer holds. The output mux prefers parked data so the held
          beat stays stable — hold rule satisfied.
        </p>
        <div class="code-block">
          <div class="code-head"><span>the line that registers the stall</span></div>
          <pre><span class="c-kw">always_comb</span>
  o_ready = ~r_valid;</pre>
        </div>
        <table class="rules">
          <thead><tr><th>Signal</th><th>In this phase</th><th>Meaning</th></tr></thead>
          <tbody>
            <tr><td><code>r_valid</code></td><td>1</td><td>Spot occupied</td></tr>
            <tr><td><code>o_ready</code></td><td>0</td><td>Tell upstream: wait</td></tr>
            <tr><td><code>o_valid</code></td><td>1</td><td>Still offering the parked beat</td></tr>
            <tr><td><code>i_ready</code></td><td>0 (for now)</td><td>Downstream still not accepting</td></tr>
          </tbody>
        </table>
      </div>

      <div class="scenario-panel card" id="panel-drain">
        <h3 style="font-family:var(--display);margin-top:0">Drain — ready returns, spot empties</h3>
        <p>
          Downstream raises <code>i_ready</code>. The parked beat transfers.
          On that clock <code>r_valid</code> clears, <code>o_ready</code> rises
          again, and you are back to pass-through.
        </p>
        <div class="callout">
          <strong>Sanity check:</strong> no beat dropped, no beat duplicated,
          and when both sides go idle the valids go idle too.
        </div>
      </div>

      <div class="scenario-panel card" id="panel-outreg">
        <h3 style="font-family:var(--display);margin-top:0">Registered outputs — <code>OPT_OUTREG=1</code></h3>
        <p>
          Same parking-spot idea, but <code>o_valid</code> / <code>o_data</code>
          are flip-flops. Helps timing when driving a long path; costs about one
          cycle of latency.
        </p>
        <div class="code-block">
          <div class="code-head"><span>only update when the output is not stalled</span></div>
          <pre><span class="c-kw">always_ff</span> @(posedge i_clk) <span class="c-kw">begin</span>
  <span class="c-kw">if</span> (i_reset)
    o_valid &lt;= 1'b0;
  <span class="c-kw">else if</span> (!o_valid || i_ready)
    o_valid &lt;= (i_valid || r_valid);
<span class="c-kw">end</span>
<span class="c-com">// same guard wraps o_data</span></pre>
        </div>
        <div class="callout warn">
          <strong>Classic bug:</strong> changing <code>o_data</code> while
          <code>o_valid &amp;&amp; !i_ready</code>. That breaks the hold rule.
        </div>
      </div>

      <div class="scenario-panel card" id="panel-lowpower">
        <h3 style="font-family:var(--display);margin-top:0">Quiet idle data — <code>OPT_LOWPOWER=1</code></h3>
        <p>
          When valid is low, force data to zero so idle buses do not toggle and
          burn power on long routes. Optional; synthesis drops the logic if the
          parameter is off.
        </p>
        <div class="code-block">
          <div class="code-head"><span>idle means quiet</span></div>
          <pre><span class="c-com">// when OPT_LOWPOWER is set:</span>
<span class="c-kw">assert property</span> (@(posedge i_clk)
  !o_valid |-&gt; (o_data == <span class="c-num">'0</span>));</pre>
        </div>
      </div>
    </section>

    <!-- CODE -->
    <section id="code">
      <div class="section-head">
        <span class="section-num">06</span>
        <h2>Reference code in this folder</h2>
      </div>
      <div class="card">
        <p style="margin-top:0">
          Open beside the projector when you want the always-blocks on screen:
        </p>
        <ul>
          <li><code>sv/skidbuffer_teaching.sv</code> — full module, heavily commented</li>
          <li><code>sv/tb_scenarios.sv</code> — pass-through, capture, recover</li>
          <li><code>sv/skidbuffer_formal_excerpt.sv</code> — rules as assertions</li>
        </ul>
        <ol class="steps">
          <li>Declare the parking spot: <code>r_valid</code>, <code>r_data</code>.</li>
          <li>Set <code>o_ready = !r_valid</code>.</li>
          <li>Capture when input accepted and output stalled; clear when drain possible.</li>
          <li>Choose comb or registered outputs with <code>OPT_OUTREG</code>.</li>
        </ol>
        <div class="code-block">
          <div class="code-head"><span>ports — VALID/READY both sides</span></div>
          <pre><span class="c-kw">module</span> skidbuffer_teaching #(
  <span class="c-kw">parameter bit</span> OPT_OUTREG   = <span class="c-num">1'b0</span>,
  <span class="c-kw">parameter bit</span> OPT_LOWPOWER = <span class="c-num">1'b0</span>,
  <span class="c-kw">parameter int</span> DW           = <span class="c-num">8</span>
) (
  <span class="c-kw">input</span>  logic          i_clk, i_reset,
  <span class="c-kw">input</span>  logic          i_valid,
  <span class="c-kw">output</span> logic          o_ready,
  <span class="c-kw">input</span>  logic [DW-1:0] i_data,
  <span class="c-kw">output</span> logic          o_valid,
  <span class="c-kw">input</span>  logic          i_ready,
  <span class="c-kw">output</span> logic [DW-1:0] o_data
);</pre>
        </div>
      </div>
    </section>

    <!-- OPTIONS -->
    <section id="options">
      <div class="section-head">
        <span class="section-num">07</span>
        <h2>Four flavors, same core</h2>
      </div>
      <div class="option-grid">
        <div class="card option-card">
          <span class="badge">OUTREG=0 · LOWPOWER=0</span>
          <h3>Comb out</h3>
          <p>Lowest latency. Best first mental model. Common on input sides.</p>
        </div>
        <div class="card option-card">
          <span class="badge">OUTREG=1 · LOWPOWER=0</span>
          <h3>Reg out</h3>
          <p>Registered outputs for easier timing on long paths.</p>
        </div>
        <div class="card option-card">
          <span class="badge">OUTREG=0 · LOWPOWER=1</span>
          <h3>Comb + quiet</h3>
          <p>Same as first, data forced to 0 when invalid.</p>
        </div>
        <div class="card option-card">
          <span class="badge">OUTREG=1 · LOWPOWER=1</span>
          <h3>Reg + quiet</h3>
          <p>Both options on — still the same parking-spot core.</p>
        </div>
      </div>
    </section>

    <!-- RULES -->
    <section id="rules">
      <div class="section-head">
        <span class="section-num">08</span>
        <h2>Rules of the road</h2>
      </div>
      <div class="card">
        <p style="margin-top:0">
          Whether or not you run a formal tool, these are the checks that mean
          “this skid is correct.”
        </p>
        <table class="rules">
          <thead>
            <tr><th>#</th><th>In English</th><th>As a property</th></tr>
          </thead>
          <tbody>
            <tr>
              <td>1</td>
              <td>Stalled output must keep the same beat.</td>
              <td><code>(o_valid &amp;&amp; !i_ready) |=&gt; (o_valid &amp;&amp; $stable(o_data))</code></td>
            </tr>
            <tr>
              <td>2</td>
              <td>Accepted-but-stalled input lands in the skid.</td>
              <td><code>... |=&gt; (r_valid &amp;&amp; r_data == $past(i_data))</code></td>
            </tr>
            <tr>
              <td>3</td>
              <td>If we stall the producer, it must hold.</td>
              <td><code>(i_valid &amp;&amp; !o_ready) |=&gt; i_valid &amp;&amp; $stable(i_data)</code></td>
            </tr>
            <tr>
              <td>4</td>
              <td>After reset, valids are low.</td>
              <td><code>i_reset |=&gt; !r_valid &amp;&amp; !o_valid</code></td>
            </tr>
          </tbody>
        </table>
      </div>
    </section>

    <!-- TAKEAWAY -->
    <section id="takeaway">
      <div class="section-head">
        <span class="section-num">09</span>
        <h2>Carry this forward</h2>
      </div>
      <div class="next-up">
        <h2>Registered stall without lost work</h2>
        <p style="margin:0 0 0.75rem;color:var(--ink-soft);font-size:1.05rem">
          Combinational stall chains hurt timing. Registering the stall is late
          by one cycle — so you need a one-slot parking spot. That is the skid.
        </p>
        <div class="key-line" style="margin:0 0 0.75rem">o_ready = !r_valid</div>
        <p style="margin:0;color:var(--ink-soft)">
          Empty → pass-through. Full → upstream waits. Drain when ready returns.
          Same idea shows up again wherever you put registered ready on a stream.
        </p>
        <p style="margin:0.85rem 0 0;font-size:0.92rem;color:var(--ink-soft)">
          Deeper dive:
          <a href="https://zipcpu.com/blog/2019/05/22/skidbuffer.html" target="_blank" rel="noopener">
            ZipCPU — Building a Skid Buffer for AXI processing
          </a>
        </p>
      </div>
    </section>

    <footer class="footer">
      <p>
        Skid buffer notes · pipeline stalls, VALID/READY, and the one-slot park.
        Companion code in <code>sv/</code>. Live walk uses <code>OPT_OUTREG=0</code>.
      </p>
    </footer>
  </main>

  <script src="js/lecture.js"></script>
</body>
</html>
