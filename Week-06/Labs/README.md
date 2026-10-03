[Assignment_Quiz.html](https://github.com/user-attachments/files/32991676/Assignment_Quiz.html)# Week 06 — Labs

This section contains the practical assignments, simulations, lab reports, and hardware design activities completed during Week 06.

==============================================================

## 1. C & Embedded C Lab Report

Practical simulation of different C and Embedded C labs using **Visual Studio Code**.

The activities focused on applying the concepts covered in the Embedded C lectures through practical programming and simulation.

[C and Embadded C Labs.pdf](https://github.com/user-attachments/files/32991632/C.and.Embadded.C.Labs.pdf)

==============================================================
### 2. Circuit Design & PCB Layout

A complete regulator design was carried out in **Altium Designer**, covering the design flow from schematic to PCB and manufacturing outputs.

**Design Objective:**

Design a regulator PCB that converts:
**5V → 3.3V**


[LM3940_Lab_Report_Professional.docx](https://github.com/user-attachments/files/32991666/LM3940_Lab_Report_Professional.docx)


==============================================================

## 3. Assignment & Lab Quiz

## Topic:Build Process, Toolchain, Porting, Linker Script & Driver Development

[U<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Assignment &amp; Lab Quiz — Toolchain, Porting, Linker, Driver Development</title>
<style>
:root{
  --bg-0:#0a0e14; --bg-1:#10151f; --bg-2:#161d2b; --bg-3:#1e2738;
  --border:#263049; --border-strong:#354061;
  --text-0:#e8edf6; --text-1:#a6b3c9; --text-2:#6e7b93;
  --teal:#2ee6c8; --teal-dim:#0f3630;
  --amber:#ffb84d; --amber-dim:#3a2a10;
  --green:#6ee7a8; --green-dim:#123527;
  --red:#ff7a7a; --red-dim:#3a1414;
  --purple:#c9a6ff;
  --code:'JetBrains Mono','Fira Code',ui-monospace,Consolas,monospace;
  --ui:-apple-system,'Segoe UI',Inter,sans-serif;
}
*{box-sizing:border-box; margin:0; padding:0;}
body{font-family:var(--ui); background:var(--bg-0); color:var(--text-0); line-height:1.55;}
button{font-family:var(--ui); cursor:pointer; color:inherit; border:none; background:none;}
input,textarea,select{font-family:var(--code); color:var(--text-0);}
code{font-family:var(--code);}

header{padding:24px 24px 12px; max-width:980px; margin:0 auto;}
header .eyebrow{font-family:var(--code); font-size:12px; color:var(--teal); letter-spacing:1.5px; font-weight:700; margin-bottom:8px;}
header h1{font-size:23px; margin-bottom:8px;}
header p{color:var(--text-1); font-size:13.5px; max-width:760px;}

.namebar{max-width:980px; margin:14px auto 0; background:var(--bg-1); border:1px solid var(--border); border-radius:12px; padding:14px 18px; display:flex; gap:14px; flex-wrap:wrap; align-items:center;}
.namebar label{font-size:12px; color:var(--text-2); margin-right:6px;}
.namebar input{background:var(--bg-2); border:1px solid var(--border-strong); border-radius:7px; padding:7px 10px; font-size:13px;}

main{max-width:980px; margin:0 auto; padding:20px 24px 40px;}
.sectiontitle{font-family:var(--code); font-size:13px; font-weight:800; color:var(--amber); letter-spacing:1px; margin:26px 0 14px; padding-bottom:8px; border-bottom:1px solid var(--border);}

.q{background:var(--bg-1); border:1px solid var(--border); border-radius:14px; padding:20px 22px; margin-bottom:14px;}
.q .qhead{display:flex; align-items:center; gap:10px; margin-bottom:8px; flex-wrap:wrap;}
.qnum{font-family:var(--code); font-weight:800; font-size:12px; color:var(--teal); background:var(--teal-dim); border-radius:6px; padding:3px 9px;}
.qpts{font-family:var(--code); font-size:10.5px; color:var(--text-2);}
.q h3{font-size:14.5px; margin:6px 0 8px;}
.q .prompt{color:var(--text-1); font-size:13px; margin-bottom:12px;}

.optrow{display:block; width:100%; text-align:left; background:var(--bg-2); border:1px solid var(--border-strong); border-radius:8px; padding:9px 12px; font-size:13px; color:var(--text-1); margin-bottom:7px;}
.optrow.selected{border-color:var(--teal); background:var(--teal-dim); color:var(--text-0);}

.tilerow{display:flex; gap:7px; flex-wrap:wrap; margin-bottom:6px;}
.tile{background:var(--bg-2); border:1px solid var(--border-strong); border-radius:8px; padding:8px 10px; display:flex; align-items:center; gap:7px; font-size:12px; font-weight:600;}
.tile button{width:20px; height:20px; border-radius:5px; background:var(--bg-3); font-size:10px; border:1px solid var(--border);}
.tile button:disabled{opacity:.3;}

.textin{width:100%; background:var(--bg-2); border:1px solid var(--border-strong); border-radius:8px; padding:8px 11px; font-size:13px;}
.numin{width:200px;}

.classrow{display:flex; justify-content:space-between; align-items:center; gap:10px; border:1px solid var(--border); border-radius:8px; padding:8px 11px; margin-bottom:6px; background:var(--bg-0);}
.classrow .txt{font-size:12.5px; flex:1;}
.classbtn{font-size:10.5px; font-weight:700; padding:5px 10px; border-radius:6px; border:1px solid var(--border-strong); background:var(--bg-2); color:var(--text-2); min-width:100px; text-align:center;}
.classbtn.state1{background:var(--teal-dim); border-color:var(--teal); color:var(--teal);}
.classbtn.state2{background:var(--amber-dim); border-color:var(--amber); color:var(--amber);}
.classsel{background:var(--bg-2); border:1px solid var(--border-strong); border-radius:6px; padding:6px 8px; font-size:12px; min-width:150px;}

.blankcode{font-family:var(--code); font-size:12px; white-space:pre-wrap; background:var(--bg-0); border:1px solid var(--border); border-radius:9px; padding:12px 14px; line-height:2;}
.blankin{background:var(--bg-3); border:1px solid var(--amber); border-radius:5px; padding:1px 6px; font-size:12px; width:110px; color:var(--amber); font-weight:700;}

.submitbar{max-width:980px; margin:0 auto 40px; background:var(--bg-1); border:2px solid var(--teal); border-radius:14px; padding:22px 24px; text-align:center;}
.btn{border-radius:9px; padding:11px 22px; font-size:13.5px; font-weight:700; transition:.15s; border:1px solid transparent;}
.btn.primary{background:var(--teal); color:#04231d;}
.btn.primary:hover{filter:brightness(1.1);}
.btn.secondary{background:var(--bg-2); color:var(--text-0); border-color:var(--border-strong);}
.btn.amber{background:var(--amber); color:#2b1c02;}
.btn:disabled{opacity:.4; cursor:not-allowed;}

.resultbox{display:none; max-width:980px; margin:0 auto 40px; background:var(--bg-1); border:2px solid var(--green); border-radius:14px; padding:26px; text-align:center;}
.resultbox.show{display:block;}
.resultbox .score{font-size:42px; font-weight:800; color:var(--green); font-family:var(--code);}
.resultbox .sub{color:var(--text-1); font-size:13.5px; margin:8px 0 18px;}
.codebox{font-family:var(--code); font-size:11.5px; background:var(--bg-0); border:1px solid var(--border); border-radius:9px; padding:14px; word-break:break-all; text-align:left; color:var(--text-1); max-height:140px; overflow:auto; margin-bottom:14px;}

.trainerlink{text-align:center; padding:20px; font-size:12px; color:var(--text-2);}
.trainerlink button{color:var(--text-2); text-decoration:underline; font-size:12px;}

.trainerpanel{display:none; max-width:1100px; margin:20px auto 60px; padding:0 24px;}
.trainerpanel.show{display:block;}
.trainerbox{background:var(--bg-1); border:2px solid var(--amber); border-radius:14px; padding:22px 24px; margin-bottom:20px;}
.trainerbox h3{color:var(--amber); margin-bottom:10px;}
.trainerrow{display:flex; gap:10px; flex-wrap:wrap; align-items:center; margin-bottom:10px;}
.trainerrow input{background:var(--bg-2); border:1px solid var(--border-strong); border-radius:8px; padding:9px 12px; font-size:13px; min-width:220px;}
textarea.codepaste{width:100%; min-height:90px; background:var(--bg-2); border:1px solid var(--border-strong); border-radius:8px; padding:10px; font-size:12px; margin-bottom:10px;}
table.roster{width:100%; border-collapse:collapse; font-size:12.5px;}
table.roster th{background:var(--bg-2); color:var(--text-2); text-align:left; padding:8px 10px; font-family:var(--code); font-size:11px;}
table.roster td{padding:8px 10px; border-top:1px solid var(--border);}
table.roster tr:hover td{background:var(--bg-2);}
.unlockmsg{font-family:var(--code); font-size:12px; margin-left:6px;}
.unlockmsg.ok{color:var(--green);} .unlockmsg.bad{color:var(--red);}
.footer-note{text-align:center; color:var(--text-2); font-size:11px; padding:10px 0 30px; font-family:var(--code);}
</style>
</head>
<body>

<header>
  <div class="eyebrow">ASSIGNMENT &amp; LAB QUIZ</div>
  <h1>Build Process, Toolchain, Porting, Linker Script &amp; Driver Development</h1>
  <p>10 quiz questions + 10 assignment tasks, fully auto-graded. Fill in your name and roll number, answer everything, then press Submit to see your score and get your submission code. Send that code to your trainer — it's how your score gets recorded, since this file works completely offline.</p>
</header>

<div class="namebar">
  <div><label>Name</label><input type="text" id="studentName" placeholder="Your full name"></div>
  <div><label>Roll #</label><input type="text" id="studentRoll" placeholder="Roll number"></div>
  <div><label>Date</label><input type="text" id="studentDate" placeholder="DD-MM-YYYY"></div>
</div>

<main>
  <div class="sectiontitle">PART 1 — QUIZ (10 questions, 1 point each)</div>
  <div id="quizContainer"></div>

  <div class="sectiontitle">PART 2 — ASSIGNMENT (10 tasks, points vary)</div>
  <div id="assignContainer"></div>
</main>

<div class="submitbar" id="submitBar">
  <button class="btn primary" onclick="submitAll()">Submit &amp; Get My Score</button>
  <div style="font-size:11.5px; color:var(--text-2); margin-top:10px;">You can only submit once your name and roll number are filled in.</div>
</div>

<div class="resultbox" id="resultBox">
  <div class="score" id="scoreDisplay"></div>
  <div class="sub" id="scoreSub"></div>
  <div style="font-size:11.5px; color:var(--text-2); margin-bottom:8px; font-family:var(--code);">YOUR SUBMISSION CODE — copy this and send it to your trainer</div>
  <div class="codebox" id="submissionCode"></div>
  <button class="btn secondary" onclick="copySubmission()">Copy Code</button>
</div>

<div class="trainerlink">
  <button onclick="toggleTrainer()">🔒 Trainer Login</button>
</div>

<div class="trainerpanel" id="trainerPanel">
  <div class="trainerbox">
    <h3>Trainer Login</h3>
    <div class="trainerrow">
      <input type="password" id="trainerPw" placeholder="Trainer password">
      <button class="btn amber" onclick="unlockTrainer()">Unlock</button>
      <span class="unlockmsg" id="unlockMsg"></span>
    </div>
  </div>

  <div class="trainerbox" id="trainerDashboard" style="display:none;">
    <h3>Add Student Submissions</h3>
    <p style="color:var(--text-1); font-size:13px; margin-bottom:10px;">Paste one or more submission codes below (one per line), collected from your students by any offline means, then click Add.</p>
    <textarea class="codepaste" id="codePaste" placeholder="Paste submission code(s) here, one per line..."></textarea>
    <div class="trainerrow">
      <button class="btn primary" onclick="addSubmissions()">Add to Roster</button>
      <button class="btn secondary" onclick="exportCsv()">⬇ Export Roster as Excel (CSV)</button>
      <button class="btn secondary" onclick="clearRoster()">Clear Roster</button>
      <span class="unlockmsg" id="addMsg"></span>
    </div>
  </div>

  <div class="trainerbox" id="rosterBox" style="display:none;">
    <h3>Roster (<span id="rosterCount">0</span> students)</h3>
    <table class="roster" id="rosterTable">
      <thead><tr><th>Name</th><th>Roll</th><th>Date</th><th>Quiz</th><th>Assignment</th><th>Total</th><th>%</th></tr></thead>
      <tbody id="rosterBody"></tbody>
    </table>
  </div>
</div>

<div class="footer-note">Fully offline — no internet or server required. Scores travel between files only through the submission code.</div>

<script>
function esc(s){ return String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;'); }
const TRAINER_PASSWORD = 'test@123';
const SALT = 'NECOP-EDU-2026-SALT';

/* ============================================================
   QUIZ DATA (10 MCQ, 1 point each)
============================================================ */
const QUIZ = [
  { q:'What does the compiler stage of the build process actually check?', opts:['Register addresses','Syntax and types','Symbol resolution across files','Physical memory layout'], a:1 },
  { q:'Which build stage would catch void init() defined in BOTH main.c and driver.c?', opts:['Preprocessor','Compiler','Assembler','Linker'], a:3 },
  { q:'What is the purpose of a cross-compiler?', opts:['Compile faster on the host machine','Produce machine code for a different CPU than the host','Compile C++ instead of C','Optimize code size only'], a:1 },
  { q:'What does OpenOCD do FIRST during the Flash step?', opts:['Erase flash sectors','Halt the CPU','Release reset','Read back to verify'], a:1 },
  { q:'In porting, which of these is Target-Specific and must change?', opts:['Application logic in main.c','Public API function names','Register addresses in the driver .c file','Function prototypes in the .h file'], a:2 },
  { q:"What does a linker script's ENTRY() directive do?", opts:['Reserves stack space','Names the label the linker/debugger treats as the program\u2019s start','Declares a memory region','Defines a new register'], a:1 },
  { q:'Why does .data need both "> RAM" and "AT > FLASH"?', opts:['It\u2019s required syntax with no real meaning','RAM stores the working copy, FLASH stores a permanent copy of the initial value','It doubles the variable\u2019s size','It tells the compiler to optimize the variable'], a:1 },
  { q:'What is the very first thing startup.S must do before almost anything else?', opts:['Call main()','Clear .bss','Set the stack pointer','Copy .data'], a:2 },
  { q:'What does the volatile keyword tell the compiler?', opts:['This variable is read-only','This value can change for reasons the compiler can\u2019t see \u2014 never optimize the read away','This variable should be stored in ROM','This variable is thread-local'], a:1 },
  { q:'Which expression clears bit n of a register?', opts:['REG(x) |= (1<<n);', 'REG(x) &= ~(1<<n);', 'REG(x) ^= (1<<n);', 'REG(x) = (1<<n);'], a:1 },
];

/* ============================================================
   ASSIGNMENT DATA (10 tasks)
============================================================ */
const ASSIGN = [
  { id:'a1', type:'reorder', title:'Order the Build Pipeline', pts:4,
    prompt:'Arrange these four stages into the correct build order.',
    items:['Linker','Source Code','Assembler','Compiler'],
    correct:['Source Code','Compiler','Assembler','Linker'] },

  { id:'a2', type:'numeric', title:'Calculate the Ported Address', pts:1,
    prompt:'Peripheral base address is 0x80000000, with each peripheral\u2019s block 0x1000 bytes apart. Your assigned peripheral, Timer, is peripheral #3. What is Timer\u2019s base address?',
    correct:'0x80003000' },

  { id:'a3', type:'classify2', title:'Portable or Target-Specific?', pts:4,
    prompt:'Classify each item. Click to cycle: unset \u2192 Portable \u2192 Target-Specific.',
    state1Label:'Portable', state2Label:'Target-Specific',
    items:[
      { text:'Application logic in main.c', correct:'state1' },
      { text:'Register addresses in the driver .c file', correct:'state2' },
      { text:'The linker script', correct:'state2' },
      { text:'The public API function names', correct:'state1' },
    ] },

  { id:'a4', type:'fillblanks', title:'Write the MEMORY Block', pts:4,
    prompt:'Chip: FLASH starts at 0x08000000, 128K in size. RAM starts at 0x20000000, 32K in size. Fill in all four values.',
    template:`MEMORY
{
  FLASH (rx)  : ORIGIN = {{B1}}, LENGTH = {{B2}}
  RAM   (rwx) : ORIGIN = {{B3}}, LENGTH = {{B4}}
}`,
    blanks:{ B1:'0x08000000', B2:'128K', B3:'0x20000000', B4:'32K' } },

  { id:'a5', type:'fillblanks', title:'Complete the SECTIONS Block', pts:4,
    prompt:'Fill in the four missing symbol names.',
    template:`.data : {
  {{B1}} = .;
  *(.data*)
  {{B2}} = .;
} > RAM AT > FLASH

.bss : {
  {{B3}} = .;
  *(.bss*)
  _bss_end = .;
} > RAM

{{B4}} = ORIGIN(RAM) + LENGTH(RAM);`,
    blanks:{ B1:'_data_start', B2:'_data_end', B3:'_bss_start', B4:'_stack_top' } },

  { id:'a6', type:'reorder', title:'Order the Boot Sequence', pts:6,
    prompt:'Arrange these six events into the order they actually happen after power-on.',
    items:['Call main()','Set the stack pointer','Power-on reset, PC jumps to _start','Loop forever if main() returns','Copy .data from FLASH to RAM','Clear .bss to zero'],
    correct:['Power-on reset, PC jumps to _start','Set the stack pointer','Copy .data from FLASH to RAM','Clear .bss to zero','Call main()','Loop forever if main() returns'] },

  { id:'a7', type:'fillblanks', title:'Complete the .bss Clearing Loop', pts:4,
    prompt:'Fill in the four missing pieces of this loop.',
    template:`    la   a0, __bss_start
    la   a1, _end
clear_loop:
    {{B1}}  a0, a1, done
    sw   {{B2}}, 0(a0)
    addi a0, a0, {{B3}}
    j    {{B4}}
done:`,
    blanks:{ B1:'bge', B2:'zero', B3:'4', B4:'clear_loop' } },

  { id:'a8', type:'mcq-multi', title:'Match Operation to Expression', pts:4,
    prompt:'For each operation, choose the matching C expression.',
    options:['REG(x) |= (1<<n);','REG(x) &= ~(1<<n);','REG(x) ^= (1<<n);','(REG(x)>>n)&0x1'],
    parts:[
      { label:'Set bit n', correct:'REG(x) |= (1<<n);' },
      { label:'Clear bit n', correct:'REG(x) &= ~(1<<n);' },
      { label:'Toggle bit n', correct:'REG(x) ^= (1<<n);' },
      { label:'Test bit n', correct:'(REG(x)>>n)&0x1' },
    ] },

  { id:'a9', type:'numeric', title:'Register Value Calculation', pts:1,
    prompt:'GPIO_OUT currently holds 0x05. You execute REG(GPIO_OUT) |= (1<<1);. What is the new value, in hex?',
    correct:'0x07' },

  { id:'a10', type:'classifyN', title:'Classify Driver Function Names', pts:4,
    prompt:'For each function, choose which pattern it follows.',
    options:['Init','Write','Read','Enable/Disable'],
    items:[
      { text:'gpio_init(pin, mode)', correct:'Init' },
      { text:'gpio_write(pin, state)', correct:'Write' },
      { text:'gpio_read(pin)', correct:'Read' },
      { text:'uart_enable()', correct:'Enable/Disable' },
    ] },
];

const MAX_QUIZ = QUIZ.length; // 1 pt each
const MAX_ASSIGN = ASSIGN.reduce((s,t)=>s+t.pts, 0);

/* ============================================================
   RENDER: QUIZ
============================================================ */
const quizAnswers = {};
function renderQuiz(){
  const wrap = document.getElementById('quizContainer');
  QUIZ.forEach((item, i)=>{
    const div = document.createElement('div');
    div.className = 'q';
    div.innerHTML = `<div class="qhead"><span class="qnum">Q${i+1}</span><span class="qpts">1 point</span></div><h3>${esc(item.q)}</h3>`;
    const optWrap = document.createElement('div');
    item.opts.forEach((opt, oi)=>{
      const b = document.createElement('button');
      b.className = 'optrow';
      b.textContent = opt;
      b.onclick = () => {
        quizAnswers[i] = oi;
        optWrap.querySelectorAll('.optrow').forEach(el=>el.classList.remove('selected'));
        b.classList.add('selected');
      };
      optWrap.appendChild(b);
    });
    div.appendChild(optWrap);
    wrap.appendChild(div);
  });
}
function gradeQuiz(){
  let score = 0;
  QUIZ.forEach((item, i)=>{ if(quizAnswers[i] === item.a) score++; });
  return score;
}

/* ============================================================
   RENDER: ASSIGNMENT (per-type renderers)
============================================================ */
const assignAnswers = {};

function renderReorderTask(task, body){
  let order = task.items.slice();
  assignAnswers[task.id] = order;
  const row = document.createElement('div');
  row.className = 'tilerow';
  body.appendChild(row);
  function draw(){
    row.innerHTML = '';
    order.forEach((label, i)=>{
      const tile = document.createElement('div');
      tile.className = 'tile';
      tile.innerHTML = `<button ${i===0?'disabled':''}>\u25C0</button><span>${esc(label)}</span><button ${i===order.length-1?'disabled':''}>\u25B6</button>`;
      const [leftBtn, , rightBtn] = tile.children;
      leftBtn.onclick = () => { [order[i-1],order[i]]=[order[i],order[i-1]]; assignAnswers[task.id]=order; draw(); };
      rightBtn.onclick = () => { [order[i+1],order[i]]=[order[i],order[i+1]]; assignAnswers[task.id]=order; draw(); };
      row.appendChild(tile);
    });
  }
  draw();
}
function gradeReorder(task){
  const given = assignAnswers[task.id] || [];
  let matches = 0;
  task.correct.forEach((val, i)=>{ if(given[i] === val) matches++; });
  return matches; // partial credit, 1 pt per correct position, max = task.pts
}

function renderNumericTask(task, body){
  const inp = document.createElement('input');
  inp.className = 'textin numin';
  inp.oninput = () => { assignAnswers[task.id] = inp.value; };
  body.appendChild(inp);
}
function gradeNumeric(task){
  const given = (assignAnswers[task.id] || '').trim().toLowerCase();
  const expected = task.correct.toLowerCase();
  const norm = s => s.replace(/^0x0*/, '0x');
  return norm(given) === norm(expected) ? task.pts : 0;
}

function renderClassify2Task(task, body){
  assignAnswers[task.id] = {};
  task.items.forEach((it, i)=>{
    const row = document.createElement('div');
    row.className = 'classrow';
    let state = '';
    const label = () => state === 'state1' ? task.state1Label : state === 'state2' ? task.state2Label : 'Click to classify';
    row.innerHTML = `<span class="txt">${esc(it.text)}</span><button class="classbtn">${label()}</button>`;
    const btn = row.querySelector('button');
    btn.onclick = () => {
      state = state === '' ? 'state1' : state === 'state1' ? 'state2' : '';
      assignAnswers[task.id][i] = state;
      btn.className = 'classbtn ' + state;
      btn.textContent = label();
    };
    body.appendChild(row);
  });
}
function gradeClassify2(task){
  const given = assignAnswers[task.id] || {};
  let score = 0;
  task.items.forEach((it, i)=>{ if(given[i] === it.correct) score++; });
  return score;
}

function renderClassifyNTask(task, body){
  assignAnswers[task.id] = {};
  task.items.forEach((it, i)=>{
    const row = document.createElement('div');
    row.className = 'classrow';
    row.innerHTML = `<span class="txt">${esc(it.text)}</span>`;
    const sel = document.createElement('select');
    sel.className = 'classsel';
    sel.innerHTML = `<option value="">\u2014 choose \u2014</option>` + task.options.map(o=>`<option value="${esc(o)}">${esc(o)}</option>`).join('');
    sel.onchange = () => { assignAnswers[task.id][i] = sel.value; };
    row.appendChild(sel);
    body.appendChild(row);
  });
}
function gradeClassifyN(task){
  const given = assignAnswers[task.id] || {};
  let score = 0;
  task.items.forEach((it, i)=>{ if(given[i] === it.correct) score++; });
  return score;
}

function renderMcqMultiTask(task, body){
  assignAnswers[task.id] = {};
  task.parts.forEach((p, i)=>{
    const row = document.createElement('div');
    row.className = 'classrow';
    row.innerHTML = `<span class="txt">${esc(p.label)}</span>`;
    const sel = document.createElement('select');
    sel.className = 'classsel';
    sel.innerHTML = `<option value="">\u2014 choose \u2014</option>` + task.options.map(o=>`<option value="${esc(o)}">${esc(o)}</option>`).join('');
    sel.onchange = () => { assignAnswers[task.id][i] = sel.value; };
    row.appendChild(sel);
    body.appendChild(row);
  });
}
function gradeMcqMulti(task){
  const given = assignAnswers[task.id] || {};
  let score = 0;
  task.parts.forEach((p, i)=>{ if(given[i] === p.correct) score++; });
  return score;
}

function renderFillBlanksTask(task, body){
  const box = document.createElement('div');
  box.className = 'blankcode';
  body.appendChild(box);
  assignAnswers[task.id] = {};
  const parts = task.template.split(/(\{\{B\d+\}\})/);
  parts.forEach(part=>{
    const m = part.match(/\{\{(B\d+)\}\}/);
    if(m){
      const bid = m[1];
      const inp = document.createElement('input');
      inp.className = 'blankin';
      inp.oninput = () => { assignAnswers[task.id][bid] = inp.value; };
      box.appendChild(inp);
    } else if(part){
      box.appendChild(document.createTextNode(part));
    }
  });
}
function gradeFillBlanks(task){
  const given = assignAnswers[task.id] || {};
  let score = 0;
  Object.keys(task.blanks).forEach(bid=>{
    if((given[bid]||'').trim() === task.blanks[bid]) score++;
  });
  return score;
}

const ASSIGN_RENDERERS = { 'reorder':renderReorderTask, 'numeric':renderNumericTask, 'classify2':renderClassify2Task, 'classifyN':renderClassifyNTask, 'mcq-multi':renderMcqMultiTask, 'fillblanks':renderFillBlanksTask };
const ASSIGN_GRADERS = { 'reorder':gradeReorder, 'numeric':gradeNumeric, 'classify2':gradeClassify2, 'classifyN':gradeClassifyN, 'mcq-multi':gradeMcqMulti, 'fillblanks':gradeFillBlanks };

function renderAssignment(){
  const wrap = document.getElementById('assignContainer');
  ASSIGN.forEach((task, i)=>{
    const div = document.createElement('div');
    div.className = 'q';
    div.innerHTML = `<div class="qhead"><span class="qnum">Task ${i+1}</span><span class="qpts">${task.pts} point${task.pts>1?'s':''}</span></div><h3>${esc(task.title)}</h3><div class="prompt">${esc(task.prompt)}</div>`;
    const body = document.createElement('div');
    div.appendChild(body);
    ASSIGN_RENDERERS[task.type](task, body);
    wrap.appendChild(div);
  });
}
function gradeAssignment(){
  let score = 0;
  ASSIGN.forEach(task=>{ score += ASSIGN_GRADERS[task.type](task); });
  return score;
}

/* ============================================================
   TAMPER-EVIDENT SUBMISSION CODE (base64 JSON + checksum)
============================================================ */
function checksum(str){
  let h = 5381;
  for(let i=0;i<str.length;i++){ h = ((h*33) ^ str.charCodeAt(i)) >>> 0; }
  const salted = (h ^ hashString(SALT)) >>> 0;
  return salted.toString(36);
}
function hashString(str){
  let h = 0;
  for(let i=0;i<str.length;i++){ h = ((h<<5)-h+str.charCodeAt(i)) | 0; }
  return h >>> 0;
}
function encodeSubmission(payload){
  const json = JSON.stringify(payload);
  const b64 = btoa(unescape(encodeURIComponent(json)));
  const check = checksum(b64);
  return b64 + '.' + check;
}
function decodeSubmission(code){
  const parts = (code || '').trim().split('.');
  if(parts.length !== 2) return null;
  const [b64, check] = parts;
  if(checksum(b64) !== check) return null; // tampered or corrupted
  try {
    const json = decodeURIComponent(escape(atob(b64)));
    return JSON.parse(json);
  } catch(e) { return null; }
}

/* ============================================================
   SUBMIT
============================================================ */
let submitted = false;
function submitAll(){
  const name = document.getElementById('studentName').value.trim();
  const roll = document.getElementById('studentRoll').value.trim();
  const date = document.getElementById('studentDate').value.trim();
  if(!name || !roll){
    alert('Please fill in your name and roll number before submitting.');
    return;
  }
  if(submitted) return;
  submitted = true;

  const quizScore = gradeQuiz();
  const assignScore = gradeAssignment();
  const total = quizScore + assignScore;
  const maxTotal = MAX_QUIZ + MAX_ASSIGN;
  const pct = Math.round((total / maxTotal) * 1000) / 10;

  const payload = {
    name, roll, date: date || new Date().toLocaleDateString(),
    quizScore, maxQuiz: MAX_QUIZ,
    assignScore, maxAssign: MAX_ASSIGN,
    total, maxTotal, pct,
    ts: new Date().toISOString(),
  };
  const code = encodeSubmission(payload);

  document.getElementById('scoreDisplay').textContent = total + ' / ' + maxTotal;
  document.getElementById('scoreSub').textContent = `Quiz: ${quizScore}/${MAX_QUIZ}  \u00b7  Assignment: ${assignScore}/${MAX_ASSIGN}  \u00b7  ${pct}%`;
  document.getElementById('submissionCode').textContent = code;
  document.getElementById('resultBox').classList.add('show');
  document.getElementById('submitBar').style.display = 'none';
  document.getElementById('resultBox').scrollIntoView({behavior:'smooth', block:'start'});
}
function copySubmission(){
  const text = document.getElementById('submissionCode').textContent;
  if(navigator.clipboard && navigator.clipboard.writeText){ navigator.clipboard.writeText(text).catch(()=>{}); }
}

/* ============================================================
   TRAINER PANEL
============================================================ */
let trainerUnlocked = false;
let roster = [];

function toggleTrainer(){
  const panel = document.getElementById('trainerPanel');
  panel.classList.toggle('show');
}
function unlockTrainer(){
  const pw = document.getElementById('trainerPw').value;
  const msg = document.getElementById('unlockMsg');
  if(pw !== TRAINER_PASSWORD){
    msg.textContent = 'Incorrect password.';
    msg.className = 'unlockmsg bad';
    return;
  }
  trainerUnlocked = true;
  msg.textContent = 'Unlocked.';
  msg.className = 'unlockmsg ok';
  document.getElementById('trainerDashboard').style.display = 'block';
  document.getElementById('rosterBox').style.display = 'block';
}
function addSubmissions(){
  const raw = document.getElementById('codePaste').value;
  const lines = raw.split('\n').map(l=>l.trim()).filter(Boolean);
  const msg = document.getElementById('addMsg');
  let added = 0, rejected = 0;
  lines.forEach(line=>{
    const data = decodeSubmission(line);
    if(!data){ rejected++; return; }
    const exists = roster.some(r => r.roll === data.roll && r.ts === data.ts);
    if(exists) return;
    roster.push(data);
    added++;
  });
  msg.textContent = `${added} added, ${rejected} rejected (invalid/tampered code).`;
  msg.className = 'unlockmsg ' + (rejected>0 ? 'bad' : 'ok');
  document.getElementById('codePaste').value = '';
  renderRoster();
}
function renderRoster(){
  const body = document.getElementById('rosterBody');
  body.innerHTML = '';
  roster.slice().sort((a,b)=> (a.roll||'').localeCompare(b.roll||'')).forEach(r=>{
    const tr = document.createElement('tr');
    tr.innerHTML = `<td>${esc(r.name)}</td><td>${esc(r.roll)}</td><td>${esc(r.date)}</td><td>${r.quizScore}/${r.maxQuiz}</td><td>${r.assignScore}/${r.maxAssign}</td><td>${r.total}/${r.maxTotal}</td><td>${r.pct}%</td>`;
    body.appendChild(tr);
  });
  document.getElementById('rosterCount').textContent = roster.length;
}
function clearRoster(){
  roster = [];
  renderRoster();
}
function exportCsv(){
  const headers = ['Name','Roll','Date','Quiz Score','Quiz Max','Assignment Score','Assignment Max','Total','Max Total','Percentage'];
  const rows = roster.slice().sort((a,b)=> (a.roll||'').localeCompare(b.roll||'')).map(r=>[
    r.name, r.roll, r.date, r.quizScore, r.maxQuiz, r.assignScore, r.maxAssign, r.total, r.maxTotal, r.pct
  ]);
  const csvLines = [headers, ...rows].map(row =>
    row.map(cell => {
      const s = String(cell);
      return /[",\n]/.test(s) ? '"' + s.replace(/"/g,'""') + '"' : s;
    }).join(',')
  );
  const csv = csvLines.join('\r\n');
  const blob = new Blob([csv], { type: 'text/csv;charset=utf-8;' });
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = 'assignment_quiz_scores.csv';
  document.body.appendChild(a);
  a.click();
  document.body.removeChild(a);
  URL.revokeObjectURL(url);
}

/* ============================================================
   INIT
============================================================ */
(function setDefaultDate(){
  const d = new Date();
  const dd = String(d.getDate()).padStart(2,'0');
  const mm = String(d.getMonth()+1).padStart(2,'0');
  document.getElementById('studentDate').value = `${dd}-${mm}-${d.getFullYear()}`;
})();
renderQuiz();
renderAssignment();
</script>
</body>
</html>
ploading Assignment_Quiz.html…]()

==============================================================
