## Below is the Lectures which we covered in the Section-02.

======================================================

## Toolchain, Porting & Driver Development Part A.

[Toolchain_Porting_Driver_Dev_Beginner_Edition_S.pptx](https://github.com/user-attachments/files/32472106/Toolchain_Porting_Driver_Dev_Beginner_Edition_S.pptx)

======================================================

## Toolchain, Porting & Driver Development Part B.

[DOC-20260801-WA0233..pptx](https://github.com/user-attachments/files/32472158/DOC-20260801-WA0233.pptx)

======================================================
## From source code to silicon, one stage at a time

[strive_build_lab.html](https://github.com/user-attachments/files/32472077/strive_build_lab.html)
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>STRIVE-I Build Lab</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;700&family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
<style>
:root{
  --bg-0:#0b0f14; --bg-1:#111826; --bg-2:#182231; --bg-3:#202c3d;
  --border:#26334a; --border-strong:#33445f;
  --text-0:#eaf0f7; --text-1:#aebdd1; --text-2:#7488a3;
  --teal:#2dd9c4; --teal-dim:#123832;
  --amber:#f5a623; --amber-dim:#3a2b0f;
  --violet:#c9a6ff; --green:#5ee6a0; --red:#ff7a7a; --blue:#6fb8ff;
  --code:'JetBrains Mono',ui-monospace,Consolas,monospace;
  --ui:'Inter',-apple-system,'Segoe UI',sans-serif;
  --radius:10px;
}
[data-theme="light"]{
  --bg-0:#f3f5f8; --bg-1:#ffffff; --bg-2:#eef1f6; --bg-3:#e4e9f0;
  --border:#d7dee8; --border-strong:#c1cbdb;
  --text-0:#131c2b; --text-1:#4c5b71; --text-2:#7c8aa0;
  --teal-dim:#e0faf6; --amber-dim:#fff2dc;
}
*{box-sizing:border-box; margin:0; padding:0;}
body{
  font-family:var(--ui); background:var(--bg-0); color:var(--text-0);
  min-height:100vh; display:flex; flex-direction:column;
}
::selection{background:var(--teal); color:#04231d;}
button{font-family:var(--ui); cursor:pointer; color:inherit;}
code, .mono{font-family:var(--code);}
a{color:var(--teal);}

/* ---------- Top bar ---------- */
.topbar{
  display:flex; align-items:center; justify-content:space-between;
  padding:12px 22px; border-bottom:1px solid var(--border);
  background:var(--bg-1); position:sticky; top:0; z-index:50;
}
.brand{display:flex; align-items:center; gap:10px;}
.brand .mark{
  width:30px; height:30px; border-radius:8px;
  background:linear-gradient(135deg, var(--teal), var(--blue));
  display:flex; align-items:center; justify-content:center;
  font-family:var(--code); font-weight:700; color:#04231d; font-size:13px;
}
.brand .name{font-weight:700; font-size:15px; letter-spacing:.2px;}
.brand .sub{font-size:11px; color:var(--text-2); font-family:var(--code); letter-spacing:.5px;}
nav.tabs{display:flex; gap:4px; background:var(--bg-2); padding:4px; border-radius:10px; border:1px solid var(--border);}
nav.tabs button{
  border:none; background:transparent; color:var(--text-1); font-size:13px; font-weight:600;
  padding:7px 14px; border-radius:7px; transition:.15s;
}
nav.tabs button.active{background:var(--bg-3); color:var(--text-0);}
nav.tabs button:hover:not(.active){color:var(--text-0);}
.top-actions{display:flex; align-items:center; gap:10px;}
.proj-pill{
  font-family:var(--code); font-size:12px; color:var(--teal);
  background:var(--teal-dim); border:1px solid var(--border); padding:5px 10px; border-radius:20px;
  display:none; align-items:center; gap:6px;
}
.proj-pill.show{display:inline-flex;}
.theme-btn{
  width:32px; height:32px; border-radius:8px; border:1px solid var(--border);
  background:var(--bg-2); color:var(--text-1); display:flex; align-items:center; justify-content:center;
  font-size:15px;
}
.theme-btn:hover{border-color:var(--border-strong); color:var(--text-0);}

main{flex:1; display:flex; flex-direction:column;}
.view{display:none; padding:28px 32px 60px; max-width:1280px; width:100%; margin:0 auto;}
.view.active{display:block;}

/* ---------- Dashboard ---------- */
.hero{
  padding:34px 32px; border-radius:16px; margin-bottom:26px;
  background:radial-gradient(circle at 15% 20%, var(--teal-dim), transparent 55%),
             radial-gradient(circle at 85% 80%, var(--amber-dim), transparent 55%),
             var(--bg-1);
  border:1px solid var(--border);
}
.hero .eyebrow{font-family:var(--code); font-size:12px; color:var(--teal); letter-spacing:1.5px; margin-bottom:10px;}
.hero h1{font-size:30px; font-weight:800; letter-spacing:-.5px; margin-bottom:10px;}
.hero p{color:var(--text-1); max-width:640px; font-size:14.5px; line-height:1.6;}

.cards{display:grid; grid-template-columns:repeat(4,1fr); gap:14px; margin:24px 0 30px;}
.card{
  background:var(--bg-1); border:1px solid var(--border); border-radius:var(--radius);
  padding:18px; transition:.15s; text-align:left; color:var(--text-0);
}
.card:hover{border-color:var(--border-strong); transform:translateY(-2px);}
.card .ic{
  width:34px; height:34px; border-radius:8px; display:flex; align-items:center; justify-content:center;
  font-size:16px; margin-bottom:12px;
}
.card h3{font-size:14.5px; font-weight:700; margin-bottom:5px; color:var(--text-0);}
.card p{font-size:12.5px; color:var(--text-2); line-height:1.5;}

.pipeline-strip{
  display:flex; align-items:center; gap:0; overflow-x:auto; padding:22px 6px;
  background:var(--bg-1); border:1px solid var(--border); border-radius:var(--radius);
}
.pnode{
  flex:0 0 auto; display:flex; flex-direction:column; align-items:center; gap:8px; padding:0 18px; position:relative;
}
.pnode .dot{
  width:46px; height:46px; border-radius:12px; background:var(--bg-2); border:1px solid var(--border-strong);
  display:flex; align-items:center; justify-content:center; font-size:18px; z-index:2;
}
.pnode span{font-size:11px; color:var(--text-1); font-weight:600; white-space:nowrap;}
.pconn{flex:1 1 30px; height:1px; background:var(--border-strong); position:relative; min-width:26px; overflow:visible;}
.pconn::after{
  content:''; position:absolute; top:-2px; left:0; width:5px; height:5px; border-radius:50%;
  background:var(--teal); animation:travel 2.6s linear infinite;
}
@keyframes travel{0%{left:0; opacity:0;}10%{opacity:1;}90%{opacity:1;}100%{left:calc(100% - 5px); opacity:0;}}

/* ---------- New Project ---------- */
.panel{background:var(--bg-1); border:1px solid var(--border); border-radius:14px; padding:26px; max-width:640px;}
.panel h2{font-size:18px; margin-bottom:4px;}
.panel .hint{color:var(--text-2); font-size:13px; margin-bottom:22px;}
.field{margin-bottom:18px;}
.field label{display:block; font-size:12.5px; font-weight:600; color:var(--text-1); margin-bottom:7px;}
.field input[type=text]{
  width:100%; background:var(--bg-2); border:1px solid var(--border); border-radius:8px; color:var(--text-0);
  padding:10px 12px; font-size:13.5px; font-family:var(--code);
}
.field input[type=text]:focus{outline:none; border-color:var(--teal);}
.chiprow{display:flex; flex-wrap:wrap; gap:8px;}
.chip{
  padding:9px 14px; border-radius:8px; border:1px solid var(--border); background:var(--bg-2);
  font-size:13px; font-weight:600; color:var(--text-1); display:flex; align-items:center; gap:7px;
}
.chip.selectable:hover{border-color:var(--border-strong);}
.chip.selected{border-color:var(--teal); color:var(--teal); background:var(--teal-dim);}
.chip.locked{opacity:.45; cursor:not-allowed;}
.btn{
  border:none; border-radius:9px; padding:11px 20px; font-size:13.5px; font-weight:700;
  background:var(--teal); color:#04231d; transition:.15s;
}
.btn:hover{filter:brightness(1.08);}
.btn.secondary{background:var(--bg-2); color:var(--text-0); border:1px solid var(--border);}
.btn.amber{background:var(--amber); color:#2b1c02;}
.btn:disabled{opacity:.4; cursor:not-allowed;}
.gen-preview{margin-top:22px; border-top:1px dashed var(--border); padding-top:18px; display:none;}
.gen-preview.show{display:block;}
.tree-line{font-family:var(--code); font-size:12.5px; color:var(--text-1); line-height:1.9;}
.tree-line b{color:var(--text-0);}

/* ---------- Explorer ---------- */
.explorer{display:grid; grid-template-columns:230px 1fr; gap:0; border:1px solid var(--border); border-radius:12px; overflow:hidden; height:600px;}
.filetree{background:var(--bg-1); border-right:1px solid var(--border); overflow-y:auto; padding:14px 8px;}
.ft-folder{font-size:12px; font-weight:700; color:var(--text-2); text-transform:uppercase; letter-spacing:.6px; padding:8px 8px 4px;}
.ft-file{
  display:flex; align-items:center; gap:8px; padding:7px 10px; border-radius:6px; font-size:13px;
  color:var(--text-1); cursor:pointer;
}
.ft-file:hover{background:var(--bg-2);}
.ft-file.active{background:var(--bg-3); color:var(--text-0); font-weight:600;}
.ft-file .fic{width:14px; text-align:center; font-size:12px;}
.codepane{background:var(--bg-0); display:flex; flex-direction:column;}
.codepane .cp-tab{
  padding:10px 16px; border-bottom:1px solid var(--border); font-family:var(--code); font-size:12.5px;
  color:var(--text-1); background:var(--bg-1); display:flex; justify-content:space-between; align-items:center;
}
.codepane .cp-body{flex:1; overflow:auto; padding:16px 0;}
.codeline{display:flex; font-family:var(--code); font-size:12.8px; line-height:1.7;}
.codeline .ln{width:42px; text-align:right; padding-right:14px; color:var(--text-2); user-select:none; flex-shrink:0;}
.codeline .txt{white-space:pre; color:var(--text-0);}
.tk-kw{color:var(--violet);} .tk-str{color:var(--amber);} .tk-com{color:var(--text-2); font-style:italic;}
.tk-num{color:var(--blue);} .tk-fn{color:var(--teal);} .tk-pre{color:var(--green);}

/* ---------- Build process ---------- */
.timeline{
  display:flex; align-items:center; gap:0; overflow-x:auto; padding:14px 10px; margin-bottom:22px;
  background:var(--bg-1); border:1px solid var(--border); border-radius:12px;
}
.tnode{
  flex:0 0 auto; padding:9px 14px; border-radius:8px; font-family:var(--code); font-size:12px; font-weight:600;
  color:var(--text-2); border:1px solid transparent; white-space:nowrap;
}
.tnode.done{color:var(--teal); background:var(--teal-dim); border-color:var(--border);}
.tnode.current{color:var(--bg-0); background:var(--teal); }
.tarrow{color:var(--border-strong); padding:0 4px; flex:0 0 auto;}

.stagegrid{display:grid; grid-template-columns:250px 1fr; gap:20px;}
.stagelist{display:flex; flex-direction:column; gap:6px;}
.stagebtn{
  text-align:left; background:var(--bg-1); border:1px solid var(--border); border-radius:9px;
  padding:11px 13px; color:var(--text-1); font-size:13px; font-weight:600;
  display:flex; align-items:center; gap:10px;
}
.stagebtn .num{
  width:22px; height:22px; border-radius:6px; background:var(--bg-2); display:flex; align-items:center;
  justify-content:center; font-size:11px; font-family:var(--code); color:var(--text-2); flex-shrink:0;
}
.stagebtn.active{border-color:var(--teal); color:var(--text-0); background:var(--teal-dim);}
.stagebtn.active .num{background:var(--teal); color:#04231d;}
.stagebtn:hover:not(.active){border-color:var(--border-strong);}

.stagepane{background:var(--bg-1); border:1px solid var(--border); border-radius:12px; padding:24px;}
.stagepane .eyebrow{font-family:var(--code); font-size:11.5px; color:var(--teal); letter-spacing:1px; margin-bottom:6px;}
.stagepane h2{font-size:19px; margin-bottom:4px;}
.io-row{display:flex; gap:10px; align-items:center; margin:14px 0 18px; font-family:var(--code); font-size:12.5px;}
.io-chip{background:var(--bg-2); border:1px solid var(--border); padding:6px 11px; border-radius:7px; color:var(--text-1);}
.io-arrow{color:var(--text-2);}
.stagepane .expl{color:var(--text-1); font-size:13.5px; line-height:1.65; margin-bottom:16px;}
.subgrid{display:grid; grid-template-columns:1fr 1fr; gap:14px; margin-bottom:16px;}
.box-lbl{font-size:11.5px; font-weight:700; color:var(--text-2); text-transform:uppercase; letter-spacing:.5px; margin-bottom:8px;}
.codebox{
  background:var(--bg-0); border:1px solid var(--border); border-radius:9px; padding:12px 14px;
  font-family:var(--code); font-size:12px; line-height:1.75; color:var(--text-0); overflow-x:auto; max-height:320px; overflow-y:auto;
  white-space:pre-wrap; word-break:break-word;
}
.codebox .hl{background:var(--teal-dim); border-radius:3px;}
.cmdline{
  font-family:var(--code); font-size:12.5px; background:var(--bg-0); border:1px solid var(--border);
  border-radius:8px; padding:11px 14px; color:var(--green); margin-bottom:16px;
}
.cmdline::before{content:'$ '; color:var(--text-2);}
.mini-tag{
  display:inline-block; font-size:11px; font-weight:700; padding:3px 8px; border-radius:5px; margin-right:6px; margin-bottom:8px;
}
.tag-tip{background:var(--amber-dim); color:var(--amber);}
.tag-mistake{background:#3a1414; color:var(--red);}
.stagepane details{margin-top:10px; border-top:1px solid var(--border); padding-top:10px;}
.stagepane summary{cursor:pointer; font-size:12.5px; font-weight:700; color:var(--text-1);}
.stagepane .detail-body{margin-top:10px; font-size:13px; color:var(--text-1); line-height:1.6;}
.detail-body ul{padding-left:18px; margin-top:6px;}
.stage-nav{display:flex; justify-content:space-between; margin-top:20px;}
.flashlog{font-family:var(--code); font-size:12.5px; line-height:2; color:var(--text-1);}
.flashlog .ok{color:var(--green);}
.flashlog .step{color:var(--teal);}
.execflow{display:flex; flex-direction:column; gap:0;}
.execnode{
  display:flex; align-items:center; gap:12px; padding:10px 14px; border-radius:9px; border:1px solid var(--border);
  background:var(--bg-0); font-family:var(--code); font-size:12.5px; margin-bottom:2px;
}
.execnode .exnum{color:var(--teal); font-weight:700;}
.execarrow-v{color:var(--text-2); padding-left:26px; font-size:13px; margin:2px 0;}

/* ---------- Toolchain ---------- */
.tc-wrap{display:grid; grid-template-columns:280px 1fr; gap:22px;}
.tc-chain{display:flex; flex-direction:column;}
.tc-node{
  background:var(--bg-1); border:1px solid var(--border); border-radius:9px; padding:11px 14px;
  font-size:13px; font-weight:600; color:var(--text-1); margin-bottom:2px;
}
.tc-node:hover{border-color:var(--border-strong); color:var(--text-0);}
.tc-node.active{border-color:var(--teal); background:var(--teal-dim); color:var(--text-0);}
.tc-arrow{text-align:center; color:var(--text-2); font-size:13px; padding:4px 0;}
.tc-detail{background:var(--bg-1); border:1px solid var(--border); border-radius:12px; padding:24px;}
.tc-detail h2{font-size:19px; margin-bottom:14px;}
.tc-detail .row{margin-bottom:14px;}
.tc-detail .row .k{font-size:11px; font-weight:700; color:var(--text-2); text-transform:uppercase; letter-spacing:.5px; margin-bottom:5px;}
.tc-detail .row .v{font-size:13.5px; color:var(--text-0); line-height:1.55;}

/* ---------- Quiz ---------- */
.quizbox{background:var(--bg-1); border:1px solid var(--border); border-radius:12px; padding:24px; margin-top:26px;}
.quizbox h3{font-size:16px; margin-bottom:16px;}
.qitem{margin-bottom:20px;}
.qitem p{font-size:13.5px; font-weight:600; margin-bottom:10px;}
.qopts{display:flex; flex-direction:column; gap:8px;}
.qopt{
  text-align:left; background:var(--bg-2); border:1px solid var(--border); border-radius:8px; padding:9px 13px;
  font-size:13px; color:var(--text-1);
}
.qopt:hover{border-color:var(--border-strong);}
.qopt.correct{border-color:var(--green); background:#0f2a1e; color:var(--green);}
.qopt.wrong{border-color:var(--red); background:#2a1414; color:var(--red);}
.qfeedback{font-size:12.5px; color:var(--text-2); margin-top:8px; display:none;}
.qfeedback.show{display:block;}

.footer-note{text-align:center; color:var(--text-2); font-size:12px; padding:20px 0; font-family:var(--code);}
.empty-state{padding:60px 20px; text-align:center; color:var(--text-2);}
.empty-state .ic{font-size:34px; margin-bottom:14px;}
@media (max-width:860px){
  .cards{grid-template-columns:1fr 1fr;} .stagegrid{grid-template-columns:1fr;} .explorer{grid-template-columns:1fr;}
  .tc-wrap{grid-template-columns:1fr;} .subgrid{grid-template-columns:1fr;}
}
</style>
</head>
<body data-theme="dark">

<div class="topbar">
  <div class="brand">
    <div class="mark">S1</div>
    <div>
      <div class="name">STRIVE-I Build Lab</div>
      <div class="sub">RISC-V EMBEDDED TOOLCHAIN SIMULATOR</div>
    </div>
  </div>
  <nav class="tabs">
    <button data-view="dashboard" class="active">Dashboard</button>
    <button data-view="newproject">New Project</button>
    <button data-view="explorer">Explorer</button>
    <button data-view="build">Build Process</button>
    <button data-view="toolchain">Toolchain</button>
  </nav>
  <div class="top-actions">
    <div class="proj-pill" id="projPill">● <span id="projPillText">no project</span></div>
    <button class="theme-btn" id="themeBtn" title="Toggle theme">☾</button>
  </div>
</div>

<main>

  <!-- ================= DASHBOARD ================= -->
  <section class="view active" id="view-dashboard">
    <div class="hero">
      <div class="eyebrow">STRIVE-I &middot; RISC-V GCC TOOLCHAIN</div>
      <h1>From source code to silicon, one stage at a time</h1>
      <p>Create a project, pick a peripheral, then step through preprocessing, compilation, assembly, linking, ELF generation, HEX/BIN packaging, flashing and execution &mdash; watching the exact same code change shape at every stage.</p>
    </div>

    <div class="cards">
      <button class="card" onclick="goto('newproject')">
        <div class="ic" style="background:var(--teal-dim); color:var(--teal);">＋</div>
        <h3>Create new project</h3>
        <p>Name it, pick a peripheral (GPIO or UART), generate a real STRIVE-I project tree.</p>
      </button>
      <button class="card" onclick="openExisting()">
        <div class="ic" style="background:var(--bg-2); color:var(--text-1);">📂</div>
        <h3>Open existing project</h3>
        <p>Reopen the project you already generated in this session.</p>
      </button>
      <button class="card" onclick="goto('build')">
        <div class="ic" style="background:var(--amber-dim); color:var(--amber);">⚙</div>
        <h3>Build process simulator</h3>
        <p>Step through all 8 build stages with real RISC-V GCC commands and output.</p>
      </button>
      <button class="card" onclick="goto('toolchain')">
        <div class="ic" style="background:var(--bg-2); color:var(--blue);">🔗</div>
        <h3>Toolchain overview</h3>
        <p>Click through every tool in the chain &mdash; purpose, input, output, command.</p>
      </button>
    </div>

    <div class="box-lbl" style="margin-bottom:10px;">Live architecture &mdash; source to silicon</div>
    <div class="pipeline-strip" id="pipelineStrip"></div>
  </section>

  <!-- ================= NEW PROJECT ================= -->
  <section class="view" id="view-newproject">
    <div class="panel">
      <h2>Create new project</h2>
      <div class="hint">Generates a complete STRIVE-I project tree with working source, matching the peripheral you pick.</div>

      <div class="field">
        <label>Project name</label>
        <input type="text" id="projName" placeholder="e.g. gpio_blink_demo" value="gpio_blink_demo">
      </div>

      <div class="field">
        <label>Target board</label>
        <div class="chiprow"><div class="chip selected">STRIVE-I &nbsp;(RV32IMC)</div></div>
      </div>

      <div class="field">
        <label>Project type &mdash; peripheral</label>
        <div class="chiprow" id="periphRow"></div>
      </div>

      <div class="field">
        <label>Toolchain</label>
        <div class="chiprow"><div class="chip selected">riscv32-unknown-elf-gcc</div></div>
      </div>

      <button class="btn" id="createBtn" onclick="createProject()">Create project</button>

      <div class="gen-preview" id="genPreview">
        <div class="box-lbl">Generated project structure</div>
        <div class="tree-line" id="genTree"></div>
        <div style="margin-top:16px;">
          <button class="btn secondary" onclick="goto('explorer')">Open in explorer →</button>
        </div>
      </div>
    </div>
  </section>

  <!-- ================= EXPLORER ================= -->
  <section class="view" id="view-explorer">
    <div id="explorerEmpty" class="empty-state">
      <div class="ic">📁</div>
      <p>No project open yet.</p>
      <div style="margin-top:14px;"><button class="btn" onclick="goto('newproject')">Create a project</button></div>
    </div>
    <div class="explorer" id="explorerMain" style="display:none;">
      <div class="filetree" id="fileTree"></div>
      <div class="codepane">
        <div class="cp-tab"><span id="cpTabName">—</span><span id="cpTabMeta" style="color:var(--text-2);"></span></div>
        <div class="cp-body" id="cpBody"></div>
      </div>
    </div>
  </section>

  <!-- ================= BUILD PROCESS ================= -->
  <section class="view" id="view-build">
    <div id="buildEmpty" class="empty-state">
      <div class="ic">⚙</div>
      <p>Create a project first &mdash; the build stages use your generated source files.</p>
      <div style="margin-top:14px;"><button class="btn" onclick="goto('newproject')">Create a project</button></div>
    </div>
    <div id="buildMain" style="display:none;">
      <div class="timeline" id="fileTimeline"></div>
      <div class="stagegrid">
        <div class="stagelist" id="stageList"></div>
        <div class="stagepane" id="stagePane"></div>
      </div>
      <div class="quizbox" id="quizBox"></div>
    </div>
  </section>

  <!-- ================= TOOLCHAIN ================= -->
  <section class="view" id="view-toolchain">
    <div class="tc-wrap">
      <div class="tc-chain" id="tcChain"></div>
      <div class="tc-detail" id="tcDetail"></div>
    </div>
  </section>

</main>

<div class="footer-note">STRIVE-I Build Lab &middot; simulated toolchain for teaching purposes &middot; all output is illustrative</div>

<script>
/* ============================================================
   THEME
============================================================ */
const themeBtn = document.getElementById('themeBtn');
themeBtn.onclick = () => {
  const b = document.body;
  const next = b.getAttribute('data-theme') === 'dark' ? 'light' : 'dark';
  b.setAttribute('data-theme', next);
  themeBtn.textContent = next === 'dark' ? '☾' : '☀';
};

/* ============================================================
   NAV
============================================================ */
document.querySelectorAll('nav.tabs button').forEach(b=>{
  b.onclick = () => goto(b.dataset.view);
});
function goto(view){
  document.querySelectorAll('.view').forEach(v=>v.classList.remove('active'));
  document.getElementById('view-'+view).classList.add('active');
  document.querySelectorAll('nav.tabs button').forEach(b=>b.classList.toggle('active', b.dataset.view===view));
  window.scrollTo({top:0, behavior:'smooth'});
}
function openExisting(){
  if(!state.project){ alert('No project generated yet in this session. Create one first.'); goto('newproject'); return; }
  goto('explorer');
}

/* ============================================================
   PIPELINE STRIP (dashboard)
============================================================ */
const PIPE_NODES = [
  ['📝','Source'],['🔧','Compiler'],['⚙','Assembler'],['🔗','Linker'],
  ['📦','ELF'],['💾','HEX/BIN'],['🔌','Programmer'],['🖥','MCU']
];
(function(){
  const el = document.getElementById('pipelineStrip');
  PIPE_NODES.forEach((n,i)=>{
    const node = document.createElement('div');
    node.className='pnode';
    node.innerHTML = `<div class="dot">${n[0]}</div><span>${n[1]}</span>`;
    el.appendChild(node);
    if(i < PIPE_NODES.length-1){
      const conn = document.createElement('div');
      conn.className='pconn';
      conn.style.setProperty('--d','none');
      el.appendChild(conn);
    }
  });
})();

/* ============================================================
   PERIPHERAL DEFINITIONS (GPIO / UART)
============================================================ */
const PERIPHERALS = {
  GPIO: {
    key:'GPIO', label:'GPIO', icon:'💡', demoLabel:'LED Blink',
    driverName:'gpio', fn:'gpio_write', initFn:'gpio_init',
    regBase:'GPIO', ledPin:19,
    files: ['main.c','gpio.c','gpio.h','startup.S','linker.ld','Makefile'],
  },
  UART: {
    key:'UART', label:'UART', icon:'🔤', demoLabel:'Serial Print',
    driverName:'uart', fn:'uart_write', initFn:'uart_init',
    regBase:'UART', ledPin:null,
    files: ['main.c','uart.c','uart.h','startup.S','linker.ld','Makefile'],
  }
};

const state = { project:null, selectedPeriph:'GPIO', currentFile:null, currentStage:0 };

function periphRow(){
  const row = document.getElementById('periphRow');
  row.innerHTML='';
  ['GPIO','UART','SPI','I2C','Timer','PWM','ADC'].forEach(p=>{
    const supported = PERIPHERALS[p];
    const div = document.createElement('div');
    div.className = 'chip ' + (supported ? 'selectable' : 'locked');
    div.textContent = p + (supported ? '' : ' (soon)');
    div.dataset.p = p;
    if(p==='GPIO') div.classList.add('selected');
    if(supported){
      div.onclick = () => {
        document.querySelectorAll('#periphRow .chip').forEach(c=>c.classList.remove('selected'));
        div.classList.add('selected');
        state.selectedPeriph = p;
      };
    }
    row.appendChild(div);
  });
  state.selectedPeriph = 'GPIO';
}
periphRow();

/* ============================================================
   FILE CONTENT GENERATORS
============================================================ */
function genMainC(p){
  if(p.key==='GPIO'){
    return `#include "gpio.h"

#define LED_PIN ${p.ledPin}

static void delay(volatile uint32_t count) {
    while (count--) { }
}

int main(void) {
    gpio_init(LED_PIN, GPIO_OUTPUT);

    while (1) {
        gpio_write(LED_PIN, HIGH);
        delay(500000);
        gpio_write(LED_PIN, LOW);
        delay(500000);
    }
    return 0;
}
`;
  }
  return `#include "uart.h"

int main(void) {
    uart_init(115200);

    while (1) {
        uart_write("Hello from STRIVE-I\\r\\n");
        for (volatile int i = 0; i < 500000; i++) { }
    }
    return 0;
}
`;
}

function genDriverH(p){
  if(p.key==='GPIO'){
    return `#ifndef GPIO_H
#define GPIO_H
#include <stdint.h>

#define GPIO_OUTPUT 0x1
#define GPIO_INPUT  0x0
#define HIGH 1
#define LOW  0

void gpio_init(uint8_t pin, uint8_t mode);
void gpio_write(uint8_t pin, uint8_t state);
uint8_t gpio_read(uint8_t pin);

#endif // GPIO_H
`;
  }
  return `#ifndef UART_H
#define UART_H
#include <stdint.h>

void uart_init(uint32_t baud);
void uart_write(const char *msg);
uint8_t uart_read(void);

#endif // UART_H
`;
}

function genDriverC(p){
  if(p.key==='GPIO'){
    return `#include "gpio.h"
#include "strive_mem_map.h"

void gpio_init(uint8_t pin, uint8_t mode) {
    if (mode == GPIO_OUTPUT)
        REG(GPIO_DIR) |= (1u << pin);
    else
        REG(GPIO_DIR) &= ~(1u << pin);
}

void gpio_write(uint8_t pin, uint8_t state) {
    if (state)
        REG(GPIO_OUT) |= (1u << pin);
    else
        REG(GPIO_OUT) &= ~(1u << pin);
}

uint8_t gpio_read(uint8_t pin) {
    return (REG(GPIO_IN) >> pin) & 0x1;
}
`;
  }
  return `#include "uart.h"
#include "strive_mem_map.h"

void uart_init(uint32_t baud) {
    REG(UART_BAUD) = SYS_CLK / baud;
    REG(UART_CTRL) = UART_ENABLE;
}

void uart_write(const char *msg) {
    while (*msg) {
        while (REG(UART_STATUS) & UART_TX_BUSY) { }
        REG(UART_TXDATA) = *msg++;
    }
}

uint8_t uart_read(void) {
    while (!(REG(UART_STATUS) & UART_RX_READY)) { }
    return (uint8_t)REG(UART_RXDATA);
}
`;
}

function genStartup(){
  return `.section .init
.global _start
_start:
    la   sp, _stack_top      # set up stack pointer
    la   t0, _bss_start
    la   t1, _bss_end
clear_bss:
    bge  t0, t1, done_bss
    sw   zero, 0(t0)
    addi t0, t0, 4
    j    clear_bss
done_bss:
    call main                # jump into C code
1:  j    1b                  # trap if main() ever returns
`;
}

function genLinker(p){
  return `MEMORY
{
  FLASH (rx)  : ORIGIN = 0x00000000, LENGTH = 128K
  RAM   (rwx) : ORIGIN = 0x80000000, LENGTH = 32K
}

ENTRY(_start)

SECTIONS
{
  .text : { *(.init) *(.text*) *(.rodata*) } > FLASH
  .data : { _data_start = .; *(.data*) _data_end = .; } > RAM AT > FLASH
  .bss  : { _bss_start = .; *(.bss*) *(COMMON) _bss_end = .; } > RAM
  _stack_top = ORIGIN(RAM) + LENGTH(RAM);
}
`;
}

function genMakefile(p, projName){
  return `PROJECT   = ${projName || 'firmware'}
CC        = riscv32-unknown-elf-gcc
OBJCOPY   = riscv32-unknown-elf-objcopy
CFLAGS    = -march=rv32imc -mabi=ilp32 -O2 -Wall -Iinclude
LDFLAGS   = -T linker.ld -nostartfiles

SRCS      = main.c ${p.driverName}.c
OBJS      = $(SRCS:.c=.o) startup.o

all: build/$(PROJECT).elf build/$(PROJECT).hex build/$(PROJECT).bin

%.o: %.c
\t$(CC) $(CFLAGS) -c $< -o build/$@

startup.o: startup.S
\t$(CC) $(CFLAGS) -c $< -o build/$@

build/$(PROJECT).elf: $(OBJS)
\t$(CC) $(LDFLAGS) $(addprefix build/,$(OBJS)) -o $@

build/$(PROJECT).hex: build/$(PROJECT).elf
\t$(OBJCOPY) -O ihex $< $@

build/$(PROJECT).bin: build/$(PROJECT).elf
\t$(OBJCOPY) -O binary $< $@

flash: build/$(PROJECT).bin
\topenocd -f interface/strive-link.cfg -f target/strive-i.cfg \\
\t        -c "program $< verify reset exit 0x00000000"

clean:
\trm -rf build/*.o build/*.elf build/*.hex build/*.bin
`;
}

/* ============================================================
   PROJECT CREATION
============================================================ */
function createProject(){
  const name = document.getElementById('projName').value.trim() || 'strive_project';
  const p = PERIPHERALS[state.selectedPeriph];
  const proj = {
    name, periph:p,
    contents:{
      'main.c': genMainC(p),
      [p.driverName+'.c']: genDriverC(p),
      [p.driverName+'.h']: genDriverH(p),
      'startup.S': genStartup(),
      'linker.ld': genLinker(p),
      'Makefile': genMakefile(p, name),
    }
  };
  state.project = proj;
  state.currentStage = 0;

  document.getElementById('projPill').classList.add('show');
  document.getElementById('projPillText').textContent = name + ' · ' + p.label;

  const preview = document.getElementById('genPreview');
  preview.classList.add('show');
  document.getElementById('genTree').innerHTML = renderTree(proj);

  buildExplorer();
  buildBuildView();
}

function renderTree(proj){
  const p = proj.periph;
  return [
    `<b>${proj.name}/</b>`,
    `├── main.c`,
    `├── ${p.driverName}.c`,
    `├── ${p.driverName}.h`,
    `├── startup.S`,
    `├── linker.ld`,
    `├── Makefile`,
    `├── include/`,
    `├── build/ &nbsp;<span style="color:var(--text-2)">(created on first build)</span>`,
    `└── output/ &nbsp;<span style="color:var(--text-2)">(created on flash export)</span>`,
  ].join('<br>');
}

/* ============================================================
   EXPLORER
============================================================ */
function tokenizeC(line){
  const esc = s => s.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;');
  const commentMatch = line.match(/(.*?)(\/\/.*)$/);
  let head = line, comment = '';
  if(commentMatch){ head = commentMatch[1]; comment = commentMatch[2]; }
  head = esc(head);
  comment = esc(comment);
  head = head.replace(/\b(void|int|char|uint8_t|uint32_t|volatile|static|return|while|if|else|const|define|include|ifndef|endif)\b/g,'<span class="tk-kw">$1</span>');
  head = head.replace(/(#\w+)/g,'<span class="tk-pre">$1</span>');
  head = head.replace(/"([^"]*)"/g,'<span class="tk-str">"$1"</span>');
  head = head.replace(/\b(0x[0-9A-Fa-f]+|\b\d+\b)/g,'<span class="tk-num">$1</span>');
  head = head.replace(/\b([a-z_][a-zA-Z0-9_]*)\s*\(/g,'<span class="tk-fn">$1</span>(');
  return head + (comment? `<span class="tk-com">${comment}</span>` : '');
}

function buildExplorer(){
  document.getElementById('explorerEmpty').style.display='none';
  document.getElementById('explorerMain').style.display='grid';
  const proj = state.project;
  const tree = document.getElementById('fileTree');
  tree.innerHTML = '';
  const folder = document.createElement('div');
  folder.className='ft-folder';
  folder.textContent = proj.name + '/';
  tree.appendChild(folder);
  Object.keys(proj.contents).forEach(fname=>{
    const row = document.createElement('div');
    row.className='ft-file';
    const ext = fname.split('.').pop();
    const icon = ext==='h' ? '🟦' : ext==='S' ? '🟨' : ext==='ld' ? '🟩' : fname==='Makefile' ? '🟧' : '🟦';
    row.innerHTML = `<span class="fic">${icon}</span><span>${fname}</span>`;
    row.onclick = () => openFile(fname);
    row.dataset.file = fname;
    tree.appendChild(row);
  });
  const buildFolder = document.createElement('div');
  buildFolder.className='ft-folder';
  buildFolder.style.marginTop='10px';
  buildFolder.textContent = 'build/ (populate via Build Process tab)';
  tree.appendChild(buildFolder);

  openFile('main.c');
}

function openFile(fname){
  document.querySelectorAll('.ft-file').forEach(f=>f.classList.toggle('active', f.dataset.file===fname));
  document.getElementById('cpTabName').textContent = fname;
  const content = state.project.contents[fname];
  document.getElementById('cpTabMeta').textContent = content.split('\n').length + ' lines · read-only';
  const body = document.getElementById('cpBody');
  body.innerHTML = '';
  content.split('\n').forEach((line,i)=>{
    const row = document.createElement('div');
    row.className='codeline';
    row.innerHTML = `<span class="ln">${i+1}</span><span class="txt">${tokenizeC(line)||'&nbsp;'}</span>`;
    body.appendChild(row);
  });
}

/* ============================================================
   BUILD STAGES DATA (generated per-project)
============================================================ */
function buildStages(){
  const proj = state.project;
  const p = proj.periph;
  const fn = p.fn, initFn = p.initFn, drv = p.driverName;

  const mainI = `# 1 "main.c"
# 1 "${drv}.h" 1
typedef unsigned char uint8_t;
typedef unsigned int  uint32_t;

extern void ${initFn}(uint8_t pin, uint8_t mode);
extern void ${fn}(uint8_t pin, uint8_t state);
extern uint8_t gpio_read(uint8_t pin);
# 2 "main.c" 2

static void delay(volatile uint32_t count) {
    while (count--) { }
}

int main(void) {
    ${initFn}(19, 0x1);

    while (1) {
        ${fn}(19, 1);
        delay(500000);
        ${fn}(19, 0);
        delay(500000);
    }
    return 0;
}`;

  const mainS = `    .text
    .globl main
main:
    addi  sp, sp, -16          # function prologue: reserve stack frame
    sw    ra, 12(sp)           # save return address
    li    a0, 19                # a0 = pin  (arg 1)
    li    a1, 1                  # a1 = mode (arg 2)
    call  ${initFn}

.L_loop:
    li    a0, 19
    li    a1, 1                  # HIGH
    call  ${fn}
    li    a0, 500000
    call  delay
    li    a0, 19
    li    a1, 0                  # LOW
    call  ${fn}
    li    a0, 500000
    call  delay
    j     .L_loop

    lw    ra, 12(sp)           # function epilogue
    addi  sp, sp, 16
    ret`;

  const objdump = `main.o:     file format elf32-littleriscv

SYMBOL TABLE:
00000000 l    d  .text  00000000 .text
00000000 g     F .text  00000034 main
00000034 g     F .text  00000018 delay
00000000         *UND*  00000000 ${initFn}
00000000         *UND*  00000000 ${fn}

RELOCATION RECORDS FOR [.text]:
OFFSET   TYPE              VALUE
00000008 R_RISCV_CALL      ${initFn}
00000018 R_RISCV_CALL      ${fn}
00000028 R_RISCV_CALL      ${fn}

Sections:
Idx Name     Size     Address
  0 .text    0000004c 00000000
  1 .data    00000000 00000000
  2 .bss     00000004 00000000
  3 .rodata  00000000 00000000`;

  const elfDump = `firmware.elf:     file format elf32-littleriscv

ELF Header:
  Entry point address:  0x00000000
  Machine:               RISC-V
  Sections:               9

Program Headers:
  LOAD  offset 0x1000  vaddr 0x00000000  filesz 0x0a40  memsz 0x0a40  R E
  LOAD  offset 0x2000  vaddr 0x80000000  filesz 0x0010  memsz 0x0040  RW

Section Headers:
  [ 1] .init      PROGBITS  00000000  size 0x00040
  [ 2] .text      PROGBITS  00000040  size 0x00a00   <- ${fn}, main, delay, startup
  [ 3] .rodata    PROGBITS  00000a40  size 0x00000
  [ 4] .data      PROGBITS  80000000  size 0x00010
  [ 5] .bss       NOBITS    80000010  size 0x00030

Symbol table '.symtab':
  00000000 FUNC   _start
  00000040 FUNC   main
  00000074 FUNC   delay
  00000090 FUNC   ${initFn}
  000000c8 FUNC   ${fn}`;

  const hexDump = `:10000000130101FF13010013050000130505... 4A
:10001000EF00408063850C00EF00801063050... 91
:100020006F0000006308050063050C0093050... 2B
:00000001FF`;

  const binDump = `00000000  13 01 01 ff 13 01 00 13  05 00 00 13 05 05 00 93
00000010  85 0c 00 ef 00 40 80 63  85 0c 00 ef 00 80 10 63
00000020  05 00 63 08 05 00 63 05  0c 00 93 05 00 00 93 05`;

  return [
    {
      key:'preprocess', num:1, title:'Preprocessing', file:'main.i',
      input:'main.c', output:'main.i',
      cmd:`riscv32-unknown-elf-gcc -E main.c -o main.i`,
      expl:`The preprocessor runs before any real compilation happens. It textually expands every <code>#include</code> (pasting in ${drv}.h's declarations), replaces every <code>#define</code> with its literal value, strips out all comments, and resolves the <code>#ifndef</code> include guard. Nothing here understands C syntax yet &mdash; it's pure text substitution.`,
      code:mainI, codeLabel:'main.i — expanded translation unit',
      tips:['Common mistake: forgetting an include guard causes "redefinition" errors once a header is included from two places.',
            'Interview question: what is the difference between a macro and a function? (Macros are expanded here, before types even exist.)'],
    },
    {
      key:'compile', num:2, title:'Compilation', file:'main.s',
      input:'main.i', output:'main.s',
      cmd:`riscv32-unknown-elf-gcc -S main.i -o main.s -march=rv32imc`,
      expl:`The compiler turns preprocessed C into RISC-V assembly &mdash; one CPU instruction per line. Function arguments are placed in registers <code>a0</code>, <code>a1</code>&hellip; per the RISC-V calling convention. Every function gets a prologue (save the stack/return address) and epilogue (restore them), and every C statement becomes one or more real instructions.`,
      code:mainS, codeLabel:'main.s — RISC-V assembly (RV32IMC)',
      tips:['Common mistake: assuming the compiler preserves your variable names &mdash; in optimized builds, locals often live only in registers and never touch memory.',
            'Interview question: why does the RISC-V calling convention reserve a0/a1 for arguments and return values?'],
    },
    {
      key:'assemble', num:3, title:'Assembly', file:'main.o',
      input:'main.s', output:'main.o',
      cmd:`riscv32-unknown-elf-as main.s -o main.o`,
      expl:`The assembler converts every instruction into its raw machine-code encoding and packages the result into an ELF object file. Calls to functions defined elsewhere (like <code>${fn}</code>, which lives in ${drv}.c) can't be resolved yet &mdash; the assembler leaves a <b>relocation entry</b> as a placeholder and records an <b>undefined symbol</b> in the symbol table for the linker to fill in later.`,
      code:objdump, codeLabel:'main.o — objdump -t (symbols + relocations)',
      tips:['Sections explained: .text = code, .data = initialized globals, .bss = zero-initialized globals (no space taken in the file), .rodata = constants.',
            'Common mistake: linking against the wrong .o and seeing "undefined reference" &mdash; that\'s an unresolved relocation, exactly like the ones shown here.'],
    },
    {
      key:'link', num:4, title:'Linking', file:'firmware.elf',
      input:`main.o + ${drv}.o + startup.o`, output:'firmware.elf',
      cmd:`riscv32-unknown-elf-gcc -T linker.ld -nostartfiles startup.o main.o ${drv}.o -o firmware.elf`,
      expl:`The linker merges every object file into one image, using <code>linker.ld</code> to decide the final address of every function and variable: code and constants go into FLASH starting at <code>0x00000000</code>, writable data goes into RAM starting at <code>0x80000000</code>. It also resolves every relocation from the previous stage &mdash; the placeholder call to <code>${fn}</code> now points at ${fn}'s real address.`,
      code:`Memory map (from linker.ld):

FLASH  0x00000000 - 0x0001FFFF  (128K)  ← .init, .text, .rodata
RAM    0x80000000 - 0x80007FFF  (32K)   ← .data, .bss, stack

Symbol resolution:
  main.o     : call ${fn}  (undefined) ─┐
  ${drv}.o${' '.repeat(Math.max(1,7-drv.length))}: ${fn} @ 0x000000c8      ├─→ resolved
  startup.o  : _start @ 0x00000000 (reset vector)  ┘

Output: firmware.elf + firmware.map (size/address report)`,
      codeLabel:'firmware.elf — memory layout & symbol resolution',
      tips:['Common mistake: forgetting -nostartfiles and getting duplicate-symbol errors against the default C runtime startup.',
            'Interview question: why must .data exist in both FLASH (its stored copy) and RAM (its runtime copy)?'],
    },
    {
      key:'elf', num:5, title:'ELF Analysis', file:'firmware.elf',
      input:'firmware.elf', output:'firmware.elf (inspected)',
      cmd:`riscv32-unknown-elf-objdump -h -t firmware.elf`,
      expl:`Before converting to a flashable image, it's worth inspecting the ELF itself. It's a rich container format: section headers, program headers (which describe LOAD segments the loader/debugger cares about), a full symbol table, and &mdash; if built with <code>-g</code> &mdash; debug information mapping every instruction back to a line of your C source. This is exactly what a debugger like GDB reads.`,
      code:elfDump, codeLabel:'firmware.elf — objdump -h -t',
      tips:['The entry point is where execution starts after reset &mdash; it points at _start in startup.S, not main() directly.',
            'Interview question: what\'s the difference between a section header and a program header? (Sections are for linking/debugging; program headers/segments are what the loader actually maps into memory.)'],
    },
    {
      key:'hexbin', num:6, title:'HEX/BIN Generation', file:'firmware.hex / firmware.bin',
      input:'firmware.elf', output:'firmware.hex, firmware.bin',
      cmd:`riscv32-unknown-elf-objcopy -O ihex firmware.elf firmware.hex\nriscv32-unknown-elf-objcopy -O binary firmware.elf firmware.bin`,
      expl:`<code>objcopy</code> strips away everything a flash chip doesn't need &mdash; symbol tables, debug info, section headers &mdash; leaving only real bytes. <b>Intel HEX</b> (.hex) is ASCII text where every line carries its own load address and a checksum, so it's self-describing and safe to hand-inspect. <b>Raw binary</b> (.bin) is just the bytes back-to-back with no addresses at all &mdash; smaller and faster to transfer, but the flashing tool must be told the start address separately.`,
      code:`firmware.hex (Intel HEX):\n${hexDump}\n\nfirmware.bin (raw bytes):\n${binDump}`,
      codeLabel:'HEX vs BIN — same program, two formats',
      tips:['Use HEX when the target address might not be obvious or the file will be shared/inspected. Use BIN for the smallest possible transfer, common with OpenOCD flashing scripts.',
            'Common mistake: flashing a .bin at the wrong address &mdash; since it carries no address info, a mistyped offset silently writes to the wrong part of flash.'],
    },
    {
      key:'flash', num:7, title:'Flash Programming', file:'→ on-chip flash',
      input:'firmware.bin', output:'bytes written to 0x00000000',
      cmd:`openocd -f interface/strive-link.cfg -f target/strive-i.cfg -c "program firmware.bin verify reset exit 0x00000000"`,
      expl:`Flashing isn't a compiler step &mdash; it's OpenOCD talking to a debug probe wired to the chip's JTAG/SWD pins. It halts the CPU so nothing interferes, erases only the flash sectors it's about to overwrite, writes the new bytes, reads them back to verify, then releases reset so the chip boots the new program.`,
      flash:true,
      tips:['Common mistake: flashing without erasing first on chips that require explicit sector erase &mdash; leftover bytes corrupt the image.',
            'Interview question: why does OpenOCD halt the CPU before writing to flash? (Flash writes are not atomic with instruction fetch on most MCUs.)'],
    },
    {
      key:'exec', num:8, title:'MCU Execution', file:'running on STRIVE-I',
      input:'flash @ 0x00000000', output:'LED blinking',
      cmd:`# no command — this happens automatically after reset`,
      expl:`The moment reset releases, the CPU fetches its very first instruction from the reset vector. From there it's a straight line down to your application code.`,
      exec:true,
      tips:['Interview question: what would happen if startup.S forgot to initialize the stack pointer before calling main()?',
            'Common mistake: relying on uninitialized globals to be zero without a working .bss clear loop in startup.S.'],
    },
  ];
}

/* ============================================================
   BUILD VIEW
============================================================ */
function buildBuildView(){
  document.getElementById('buildEmpty').style.display='none';
  document.getElementById('buildMain').style.display='block';
  state.stages = buildStages();
  renderStageList();
  renderTimeline();
  showStage(0);
  renderQuiz();
}

function renderStageList(){
  const list = document.getElementById('stageList');
  list.innerHTML='';
  state.stages.forEach((s,i)=>{
    const btn = document.createElement('button');
    btn.className = 'stagebtn' + (i===state.currentStage ? ' active':'');
    btn.innerHTML = `<span class="num">${s.num}</span><span>${s.title}</span>`;
    btn.onclick = () => showStage(i);
    list.appendChild(btn);
  });
}

function renderTimeline(){
  const tl = document.getElementById('fileTimeline');
  tl.innerHTML='';
  const chain = ['main.c', ...state.stages.map(s=>s.file)];
  chain.forEach((f,i)=>{
    const stageIdx = i-1;
    const node = document.createElement('div');
    node.className = 'tnode';
    if(stageIdx < state.currentStage) node.classList.add('done');
    if(stageIdx === state.currentStage) node.classList.add('current');
    node.textContent = f;
    if(stageIdx >=0){
      node.style.cursor='pointer';
      node.onclick = () => showStage(stageIdx);
    }
    tl.appendChild(node);
    if(i < chain.length-1){
      const arrow = document.createElement('div');
      arrow.className='tarrow';
      arrow.textContent='→';
      tl.appendChild(arrow);
    }
  });
}

function showStage(i){
  state.currentStage = i;
  renderStageList();
  renderTimeline();
  const s = state.stages[i];
  const pane = document.getElementById('stagePane');

  let bodyHtml = '';
  if(s.flash){
    bodyHtml = `
      <div class="io-row">
        <div class="io-chip">PC</div><div class="io-arrow">→</div>
        <div class="io-chip">OpenOCD</div><div class="io-arrow">→</div>
        <div class="io-chip">JTAG / SWD</div><div class="io-arrow">→</div>
        <div class="io-chip">STRIVE-I MCU</div><div class="io-arrow">→</div>
        <div class="io-chip">Flash memory</div>
      </div>
      <div class="cmdline">${s.cmd}</div>
      <div class="box-lbl">OpenOCD session log</div>
      <div class="codebox flashlog">
        <div><span class="step">[strive-link]</span> connected, SWD speed 4000 kHz</div>
        <div><span class="step">[target]</span> halting CPU&hellip; <span class="ok">halted</span></div>
        <div><span class="step">[flash]</span> erasing sectors 0x00000000&ndash;0x00001000&hellip; <span class="ok">erased</span></div>
        <div><span class="step">[flash]</span> writing 2624 bytes @ 0x00000000&hellip; <span class="ok">done</span></div>
        <div><span class="step">[flash]</span> verifying image&hellip; <span class="ok">match</span></div>
        <div><span class="step">[target]</span> releasing reset&hellip; <span class="ok">running</span></div>
      </div>`;
  } else if(s.exec){
    const nodes = [
      ['1','Reset vector','CPU fetches its first instruction from 0x00000000'],
      ['2','Startup code','startup.S sets the stack pointer and clears .bss'],
      ['3','main()','control jumps into your C entry point'],
      [`4`, `${state.project.periph.initFn}()`, `pin ${state.project.periph.ledPin||''} configured as output`.replace('  ',' ')],
      ['5', state.project.periph.key==='GPIO' ? 'LED blink loop' : 'UART print loop', state.project.periph.key==='GPIO' ? `${state.project.periph.fn}() toggles the pin every 500k cycles` : `${state.project.periph.fn}() sends a string every loop`],
    ];
    bodyHtml = `<div class="execflow">` + nodes.map((n,idx)=>
      `<div class="execnode"><span class="exnum">${n[0]}</span><b>${n[1]}</b><span style="color:var(--text-2)">— ${n[2]}</span></div>`
      + (idx<nodes.length-1 ? `<div class="execarrow-v">↓</div>` : '')
    ).join('') + `</div>`;
  } else {
    bodyHtml = `
      <div class="io-row">
        <div class="io-chip">${s.input}</div><div class="io-arrow">→</div><div class="io-chip">${s.output}</div>
      </div>
      <div class="cmdline">${s.cmd.replace(/\n/g,'<br>')}</div>
      <div class="box-lbl">${s.codeLabel}</div>
      <div class="codebox">${escapeHtml(s.code)}</div>`;
  }

  pane.innerHTML = `
    <div class="eyebrow">BUILD PROCESS · STAGE ${s.num} OF 8</div>
    <h2>${s.title}</h2>
    <div class="expl">${s.expl}</div>
    ${bodyHtml}
    <details>
      <summary>Learning notes, common mistakes & interview questions</summary>
      <div class="detail-body">
        <ul>${s.tips.map(t=>`<li>${t}</li>`).join('')}</ul>
      </div>
    </details>
    <div class="stage-nav">
      <button class="btn secondary" ${i===0?'disabled':''} onclick="showStage(${i-1})">← Previous stage</button>
      <button class="btn" ${i===state.stages.length-1?'disabled':''} onclick="showStage(${i+1})">Next stage →</button>
    </div>
  `;
}

function escapeHtml(s){
  return s.replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;');
}

/* ============================================================
   QUIZ
============================================================ */
const QUIZ = [
  { q:'Which file is produced right after the assembler runs?', opts:['main.i','main.s','main.o','firmware.elf'], a:2,
    exp:'The assembler turns main.s into main.o — a relocatable object file with unresolved symbols.' },
  { q:'What does the linker script (linker.ld) actually decide?', opts:['Variable names','Where in memory each section is placed','Which compiler to use','The clock speed'], a:1,
    exp:'The linker script maps sections like .text and .data to real FLASH/RAM addresses.' },
  { q:'Why generate both a .hex and a .bin from the same firmware.elf?', opts:['They contain different code','HEX is self-describing with addresses; BIN is raw bytes only','BIN is for debugging, HEX is not','There is no real difference'], a:1,
    exp:'Same bytes, different packaging — HEX embeds addresses and checksums, BIN is the smallest possible raw transfer.' },
  { q:'What does OpenOCD do immediately before writing to flash?', opts:['Compiles the code','Halts the CPU','Reboots your PC','Deletes the .elf file'], a:1,
    exp:'The CPU is halted first so nothing executes while flash memory is being erased and rewritten underneath it.' },
];

function renderQuiz(){
  const box = document.getElementById('quizBox');
  box.innerHTML = `<h3>Quick check — 4 questions</h3>` + QUIZ.map((item,qi)=>`
    <div class="qitem">
      <p>${qi+1}. ${item.q}</p>
      <div class="qopts">
        ${item.opts.map((o,oi)=>`<button class="qopt" onclick="answerQuiz(${qi},${oi},this)">${o}</button>`).join('')}
      </div>
      <div class="qfeedback" id="qf-${qi}">${item.exp}</div>
    </div>
  `).join('');
}
function answerQuiz(qi, oi, btn){
  const item = QUIZ[qi];
  const opts = btn.parentElement.querySelectorAll('.qopt');
  opts.forEach((o,i)=>{
    o.disabled = true;
    if(i===item.a) o.classList.add('correct');
    else if(i===oi) o.classList.add('wrong');
  });
  document.getElementById('qf-'+qi).classList.add('show');
}

/* ============================================================
   TOOLCHAIN VIEW
============================================================ */
const TOOLCHAIN = [
  { name:'Source code', purpose:'The C/assembly you write — main.c, driver .c/.h files.', input:'You, typing', output:'.c / .h / .S files', cmd:'—' },
  { name:'Preprocessor', purpose:'Expands #include and #define, strips comments, resolves include guards.', input:'main.c', output:'main.i', cmd:'riscv32-unknown-elf-gcc -E main.c -o main.i' },
  { name:'Compiler', purpose:'Translates preprocessed C into RISC-V assembly.', input:'main.i', output:'main.s', cmd:'riscv32-unknown-elf-gcc -S main.i -o main.s' },
  { name:'Assembler', purpose:'Turns assembly into machine code inside a relocatable object file.', input:'main.s', output:'main.o', cmd:'riscv32-unknown-elf-as main.s -o main.o' },
  { name:'Object files', purpose:'One .o per source file, each with unresolved references to functions defined elsewhere.', input:'every .c / .S', output:'main.o, gpio.o, startup.o', cmd:'—' },
  { name:'Libraries', purpose:'Precompiled code (libc stubs, math routines) the linker can pull symbols from.', input:'toolchain-provided .a archives', output:'linked-in object code', cmd:'-lc -lm (implicit)' },
  { name:'Linker', purpose:'Merges every object file + library into one image, resolving every address.', input:'*.o + linker.ld', output:'firmware.elf', cmd:'riscv32-unknown-elf-gcc -T linker.ld *.o -o firmware.elf' },
  { name:'ELF', purpose:'Rich container: sections, symbols, debug info, program headers — what a debugger reads.', input:'firmware.elf (just linked)', output:'inspected via objdump/gdb', cmd:'riscv32-unknown-elf-objdump -h -t firmware.elf' },
  { name:'Objcopy', purpose:'Strips debug/symbol info, keeping only the bytes that belong in flash.', input:'firmware.elf', output:'firmware.hex / firmware.bin', cmd:'riscv32-unknown-elf-objcopy -O binary firmware.elf firmware.bin' },
  { name:'HEX / BIN', purpose:'The two common flashable formats — HEX is address-tagged ASCII, BIN is raw bytes.', input:'firmware.elf', output:'ready-to-flash image', cmd:'—' },
  { name:'OpenOCD / Programmer', purpose:'Talks to the debug probe over JTAG/SWD to erase, write and verify flash.', input:'firmware.bin', output:'bytes written to chip', cmd:'openocd -f interface/strive-link.cfg -f target/strive-i.cfg -c "program firmware.bin verify reset exit"' },
  { name:'STRIVE-I flash', purpose:'Non-volatile memory on-chip. On reset, the CPU starts executing from here.', input:'flash contents', output:'your program, running', cmd:'—' },
];

function buildToolchainView(){
  const chain = document.getElementById('tcChain');
  chain.innerHTML='';
  TOOLCHAIN.forEach((t,i)=>{
    const node = document.createElement('div');
    node.className='tc-node' + (i===0?' active':'');
    node.textContent = t.name;
    node.onclick = () => showTc(i);
    chain.appendChild(node);
    if(i<TOOLCHAIN.length-1){
      const arrow = document.createElement('div');
      arrow.className='tc-arrow'; arrow.textContent='↓';
      chain.appendChild(arrow);
    }
  });
  showTc(0);
}
function showTc(i){
  document.querySelectorAll('.tc-node').forEach((n,ni)=>n.classList.toggle('active', ni===i));
  const t = TOOLCHAIN[i];
  document.getElementById('tcDetail').innerHTML = `
    <h2>${t.name}</h2>
    <div class="row"><div class="k">Purpose</div><div class="v">${t.purpose}</div></div>
    <div class="row"><div class="k">Input</div><div class="v mono">${t.input}</div></div>
    <div class="row"><div class="k">Output</div><div class="v mono">${t.output}</div></div>
    <div class="row"><div class="k">Command</div><div class="v"><div class="cmdline" style="margin:0;">${t.cmd}</div></div></div>
  `;
}
buildToolchainView();
</script>
</body>
</html>





