[ram_flash_guided_lesson.html](https://github.com/user-attachments/files/32473285/ram_flash_guided_lesson.html)[lab_2hour_exercise.html](https://github.com/user-attachments/files/32473240/lab_2hour_exercise.html)[complete_the_files_lab.html](https://github.com/user-attachments/files/32473095/complete_the_files_lab.html)## Below is the Lectures which we covered in the Section-02.

======================================================

## Toolchain, Porting & Driver Development Part A.

[Toolchain_Porting_Driver_Dev_Beginner_Edition_S.pptx](https://github.com/user-attachments/files/32472106/Toolchain_Porting_Driver_Dev_Beginner_Edition_S.pptx)

======================================================

## Toolchain, Porting & Driver Development Part B.

[DOC-20260801-WA0233..pptx](https://github.com/user-attachments/files/32472158/DOC-20260801-WA0233.pptx)

======================================================

## START 
## Fill in what's missing — then regenerate the complete files

<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Complete Your Own linker.ld &amp; startup.S — Lab</title>
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
input{font-family:var(--code);}
code{font-family:var(--code);}

header{padding:26px 24px 8px; max-width:1240px; margin:0 auto;}
header .eyebrow{font-family:var(--code); font-size:12px; color:var(--teal); letter-spacing:1.5px; font-weight:700; margin-bottom:8px;}
header h1{font-size:24px; margin-bottom:8px;}
header p{color:var(--text-1); font-size:14px; max-width:760px;}

main{max-width:1240px; margin:0 auto; padding:14px 24px 60px;}

.tabs{display:flex; gap:8px; margin-bottom:16px;}
.tabbtn{
  padding:10px 20px; border-radius:9px 9px 0 0; font-size:13.5px; font-weight:700; background:var(--bg-1);
  border:1px solid var(--border); border-bottom:none; color:var(--text-2);
}
.tabbtn.active{background:var(--bg-2); color:var(--teal); border-color:var(--border-strong);}

.filewrap{display:none;}
.filewrap.active{display:block;}
.layout{display:grid; grid-template-columns:1fr 400px; gap:18px; align-items:start;}
@media (max-width:980px){ .layout{grid-template-columns:1fr;} }

.codepanel{background:var(--bg-2); border:1px solid var(--border-strong); border-radius:0 12px 12px 12px; padding:18px 20px; max-height:640px; overflow:auto;}
.codeline{font-family:var(--code); font-size:12px; line-height:1.85; white-space:pre-wrap; word-break:break-word; color:var(--text-0);}
.tk-kw{color:var(--purple);} .tk-com{color:var(--text-2); font-style:italic;} .tk-num{color:#7ab8ff;} .tk-reg{color:var(--amber);} .tk-lbl{color:var(--green);} .tk-dir{color:#7ab8ff;}
.blankchip{
  display:inline-block; min-width:52px; padding:1px 8px; border-radius:5px; background:var(--amber-dim); border:1px solid var(--amber);
  color:var(--amber); font-weight:800; font-size:11.5px; text-align:center;
}
.blankchip.correct{background:var(--green-dim); border-color:var(--green); color:var(--green);}
.blankchip.wrong{background:var(--red-dim); border-color:var(--red); color:var(--red);}
.blankchip.empty{background:var(--bg-3); border-color:var(--border-strong); color:var(--text-2);}

.qpanel{background:var(--bg-1); border:1px solid var(--border); border-radius:12px; padding:16px; max-height:640px; overflow:auto;}
.qpanel h3{font-size:14px; color:var(--teal); margin-bottom:12px; font-family:var(--code);}
.qitem{border:1px solid var(--border); border-radius:9px; padding:12px 14px; margin-bottom:10px; background:var(--bg-0);}
.qitem .qnum{font-family:var(--code); font-size:10.5px; font-weight:800; color:var(--amber); margin-bottom:5px;}
.qitem .qhint{font-size:12.5px; color:var(--text-1); margin-bottom:9px;}
.qitem input{
  width:100%; background:var(--bg-2); border:1px solid var(--border-strong); border-radius:7px; padding:8px 10px;
  font-size:12.5px; color:var(--text-0);
}
.qitem input:focus{outline:none; border-color:var(--teal);}
.qitem input.correct{border-color:var(--green); background:var(--green-dim);}
.qitem input.wrong{border-color:var(--red); background:var(--red-dim);}

.controls{display:flex; gap:10px; align-items:center; margin-top:14px; flex-wrap:wrap;}
.btn{border-radius:9px; padding:10px 18px; font-size:13px; font-weight:700; transition:.15s; border:1px solid transparent;}
.btn.primary{background:var(--teal); color:#04231d;}
.btn.primary:hover{filter:brightness(1.1);}
.btn.secondary{background:var(--bg-2); color:var(--text-0); border-color:var(--border-strong);}
.btn.secondary:hover{border-color:var(--teal); color:var(--teal);}
.btn:disabled{opacity:.35; cursor:not-allowed;}
.status{font-family:var(--code); font-size:12.5px; color:var(--text-2);}
.status.ok{color:var(--green);}
.status.bad{color:var(--red);}

.generated{display:none; margin-top:26px; background:var(--bg-1); border:1px solid var(--green); border-radius:12px; padding:20px;}
.generated.show{display:block; animation:fadeIn .4s ease;}
@keyframes fadeIn{ from{opacity:0; transform:translateY(8px);} to{opacity:1; transform:translateY(0);} }
.generated h3{color:var(--green); margin-bottom:10px; font-size:15px;}
.generated .codebox{font-family:var(--code); font-size:11.5px; white-space:pre-wrap; word-break:break-word; background:var(--bg-0); border:1px solid var(--border); border-radius:10px; padding:14px 16px; max-height:400px; overflow:auto; color:var(--text-0); margin-bottom:10px;}
.copybtn{font-size:11.5px; padding:6px 12px;}

.footer-note{text-align:center; color:var(--text-2); font-size:11px; padding:20px 0; font-family:var(--code);}
</style>
</head>
<body>

<header>
  <div class="eyebrow">LAB · COMPLETE THE REAL FILE</div>
  <h1>Fill in what's missing — then regenerate the complete files</h1>
  <p>This is your actual <code>linker.ld</code> and <code>startup.S</code> — the real SweRV RISC-V files, not a simplified example. Most of it is already here. Answer the questions on the right using what you already know, and each answer fills in the matching blank in the code.</p>
</header>

<main>
  <div class="tabs">
    <button class="tabbtn active" id="tabLinker" onclick="switchTab('linker')">linker.ld <span id="linkerBadge" style="color:var(--text-2); font-weight:400;"></span></button>
    <button class="tabbtn" id="tabStartup" onclick="switchTab('startup')">startup.S <span id="startupBadge" style="color:var(--text-2); font-weight:400;"></span></button>
  </div>

  <div class="filewrap active" id="wrap-linker">
    <div class="layout">
      <div class="codepanel" id="code-linker"></div>
      <div class="qpanel"><h3>QUESTIONNAIRE — linker.ld</h3><div id="q-linker"></div></div>
    </div>
    <div class="controls">
      <button class="btn primary" onclick="checkAnswers('linker')">Check my answers</button>
      <button class="btn secondary" onclick="revealAll('linker')">Give up — show answers</button>
      <span class="status" id="status-linker"></span>
    </div>
  </div>

  <div class="filewrap" id="wrap-startup">
    <div class="layout">
      <div class="codepanel" id="code-startup"></div>
      <div class="qpanel"><h3>QUESTIONNAIRE — startup.S</h3><div id="q-startup"></div></div>
    </div>
    <div class="controls">
      <button class="btn primary" onclick="checkAnswers('startup')">Check my answers</button>
      <button class="btn secondary" onclick="revealAll('startup')">Give up — show answers</button>
      <span class="status" id="status-startup"></span>
    </div>
  </div>

  <div class="controls" style="margin-top:10px;">
    <button class="btn primary" id="genBtn" onclick="generateFiles()" disabled>🎉 Generate the complete files</button>
    <span class="status" id="genStatus">Complete both files above with all-correct answers to unlock this.</span>
  </div>

  <div class="generated" id="generatedBox">
    <h3>Your complete, regenerated linker.ld</h3>
    <div class="codebox" id="finalLinker"></div>
    <button class="btn secondary copybtn" onclick="copyText('finalLinker')">Copy linker.ld</button>
    <h3 style="margin-top:22px;">Your complete, regenerated startup.S</h3>
    <div class="codebox" id="finalStartup"></div>
    <button class="btn secondary copybtn" onclick="copyText('finalStartup')">Copy startup.S</button>
  </div>
</main>

<div class="footer-note">Every line not blanked out is exactly your original file, unchanged.</div>

<script>
function esc(s){ return String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;'); }

/* ============================================================
   FILE DATA — real linker.ld and startup.S, with {{Bn}} blanks
============================================================ */
const LINKER_TEMPLATE = `OUTPUT_ARCH( "riscv" )

ENTRY( {{B1}} )

MEMORY
{
  ram  (wxa!ri) : ORIGIN = {{B2}}, LENGTH = {{B3}}
}

PHDRS
{
  rom_load PT_LOAD;
  ram_init PT_LOAD;
  {{B4}} PT_LOAD;
}

SECTIONS
{
  __stack_size = DEFINED(__stack_size) ? __stack_size : 4K;

  .text.init :
  {
    *(.text.init)
    . = ALIGN(8);
  } > ram : ram_load

  .text :
  {
    *(.text.unlikely .text.unlikely.*)
    *(.text.startup .text.startup.*)
    *(.text .text.*)
    *(.gnu.linkonce.t.*)
    . = ALIGN(4);
  } > ram : ram_load

  .rodata :
  {
    *(.rdata)
    *(.rodata .rodata.*)
    *(.gnu.linkonce.r.*)
    . = ALIGN(4);
  } > ram : ram_load

  .lalign :
  {
    . = ALIGN(4);
    PROVIDE( _data_lma = {{B5}} );
  } > ram : ram_load

  .dalign :
  {
    . = ALIGN(4);
    PROVIDE( _data = . );
  } > ram : ram_load

  .data :
  {
    *(.data .data.*)
    *(.gnu.linkonce.d.*)
    . += 10;
    . = ALIGN(8);
  } > ram : ram_load

  .sdata :
  {
    . = ALIGN(8);
    __global_pointer$ = . + {{B6}};
    *(.sdata .sdata.*)
    *(.gnu.linkonce.s.*)
    . = ALIGN(8);
    *(.srodata .srodata.*)
    . = ALIGN(8);
  } > ram : ram_load

  . = ALIGN(4);
  PROVIDE( _edata = . );
  PROVIDE( edata = . );

  PROVIDE( _fbss = . );
  PROVIDE( {{B7}} = . );

  .bss :
  {
    *(.sbss .sbss.* .gnu.linkonce.sb.*)
    *(.scommon)
    *(.bss)
    . = ALIGN(8);
  } > ram : ram_load

  {{B8}} = .;

  .stack :
  {
    _heap_end = .;
    . = . + __stack_size;
    {{B9}} = .;
  } > ram : ram_load
}`;

const LINKER_BLANKS = {
  B1: { answer:'_start', hint:'Which label does startup.S define with .global as its very first instruction after reset?' },
  B2: { answer:'0x00000000', hint:"This chip's only memory region starts at the very first possible address. In hex, what does \"address zero\" look like?", lenientHex:true },
  B3: { answer:'64K', hint:'The datasheet says this chip has 64 kilobytes of RAM. How do you write that using the linker script\u2019s shorthand?' },
  B4: { answer:'ram_load', hint:'Every SECTIONS rule below ends with "> ram : ___". Which PHDRS name, already declared just above, do they all actually use?' },
  B5: { answer:'.', hint:'What single character means "the current address, right now, as the linker lays things out"?' },
  B6: { answer:'0x800', hint:'RISC-V\u2019s global-pointer trick centers a small window of fast-reachable addresses. The standard convention offsets it by 2048 bytes \u2014 write that as hex.', lenientHex:true },
  B7: { answer:'__bss_start', hint:'What name will startup.S look for \u2014 via "la a0, ___" \u2014 to know where zero-clearing should begin?' },
  B8: { answer:'_end', hint:'What symbol marks "the end of all the static, unmoving memory" \u2014 right after .bss finishes?' },
  B9: { answer:'_sp', hint:'What symbol does startup.S load directly into the stack pointer register with "la sp, ___"?' },
};

const STARTUP_TEMPLATE = `  .section ".text.init"
  .global {{B10}}
  .type   _start, @function

_start:
  csrw minstret, zero
  csrw minstreth, zero

  li  x1, 0
  li  x2, 0
  /* ... x3 through x30 cleared to 0 the same way ... */
  li  x31,0

  li t1, 0x55555555
  csrw 0x7c0, t1          # chip-specific cache configuration

  .option push
  .option norelax
  la gp, __global_pointer$
  .option pop
  la sp, {{B11}}

  /* Clear bss section */
  la a0, {{B12}}
  la a1, {{B13}}
  bgeu a0, a1, 2f
1:
  sw {{B14}}, (a0)
  addi a0, a0, 4
  bltu a0, a1, 1b
2:

  call __libc_init_array

  li a0, 0
  li a1, 0

  call {{B15}}

 2:  j {{B16}}`;

const STARTUP_BLANKS = {
  B10: { answer:'_start', hint:'Which exact label is defined a few lines below, and must match ENTRY() in linker.ld?' },
  B11: { answer:'_sp', hint:'Which symbol \u2014 calculated inside linker.ld\u2019s .stack section \u2014 does the stack pointer get loaded from?' },
  B12: { answer:'__bss_start', hint:'Which symbol marks where the zero-clearing loop should start reading from?' },
  B13: { answer:'_end', hint:'Which symbol marks where the zero-clearing loop should stop?' },
  B14: { answer:'zero', hint:'Which RISC-V register always reads as the literal value 0 \u2014 used here so nothing has to be loaded first?' },
  B15: { answer:'main', hint:'After every setup step above is done, which C function does startup.S finally hand control to?' },
  B16: { answer:'2b', hint:'This line must jump backward, forever, to a label already defined above. Local labels use a direction suffix \u2014 "b" for backward, "f" for forward. Which label number, with which suffix, makes this loop right here?' },
};

/* ============================================================
   SINGLE-PASS TOKENIZER + BLANK RENDERING (safe — one pass, no re-scanning)
============================================================ */
function tokenizeLine(line, blanks, answers){
  const commentMatch = line.match(/(\/\*.*?\*\/|#.*$)/);
  const KEYWORDS = 'ENTRY|MEMORY|PHDRS|SECTIONS|PT_LOAD|ORIGIN|LENGTH|PROVIDE|DEFINED|ALIGN';
  const tokenRe = new RegExp(
    '(\\{\\{B\\d+\\}\\})' + '|' +
    '(/\\*.*?\\*/|#.*$)' + '|' +
    '\\b(' + KEYWORDS + ')\\b' + '|' +
    '(\\.[a-zA-Z_][\\w.]*)' + '|' +
    '\\b(0x[0-9A-Fa-f]+|\\d+K?)\\b' + '|' +
    '\\b(la|lw|sw|call|j|bgeu|bltu|addi|li|csrw|ret)\\b' + '|' +
    '\\b(zero|a[0-7]|t[0-6]|sp|gp|x\\d+)\\b',
    'g'
  );
  let out = '', last = 0, m;
  while((m = tokenRe.exec(line)) !== null){
    out += esc(line.slice(last, m.index));
    if(m[1]){
      const bid = m[1].replace(/[{}]/g,'');
      const val = answers[bid];
      const cls = val === undefined || val === '' ? 'empty' : 'pending';
      out += `<span class="blankchip ${cls}" id="chip-${bid}">${val ? esc(val) : bid}</span>`;
    }
    else if(m[2]) out += `<span class="tk-com">${esc(m[2])}</span>`;
    else if(m[3]) out += `<span class="tk-kw">${esc(m[3])}</span>`;
    else if(m[4]) out += `<span class="tk-dir">${esc(m[4])}</span>`;
    else if(m[5]) out += `<span class="tk-num">${esc(m[5])}</span>`;
    else if(m[6]) out += `<span class="tk-kw">${esc(m[6])}</span>`;
    else if(m[7]) out += `<span class="tk-reg">${esc(m[7])}</span>`;
    last = tokenRe.lastIndex;
  }
  out += esc(line.slice(last));
  return out || '&nbsp;';
}

const answersStore = { linker:{}, startup:{} };

function renderCode(fileKey, template, blanksMap){
  const box = document.getElementById('code-' + fileKey);
  box.innerHTML = '';
  template.split('\n').forEach(line=>{
    const div = document.createElement('div');
    div.className = 'codeline';
    div.innerHTML = tokenizeLine(line, blanksMap, answersStore[fileKey]);
    box.appendChild(div);
  });
}

function renderQuestionnaire(fileKey, blanksMap){
  const wrap = document.getElementById('q-' + fileKey);
  wrap.innerHTML = '';
  Object.keys(blanksMap).forEach((bid, i)=>{
    const b = blanksMap[bid];
    const item = document.createElement('div');
    item.className = 'qitem';
    item.innerHTML = `
      <div class="qnum">QUESTION ${i+1} &middot; blank ${bid}</div>
      <div class="qhint">${esc(b.hint)}</div>
      <input type="text" id="input-${bid}" placeholder="type your answer" autocomplete="off" spellcheck="false">
    `;
    wrap.appendChild(item);
    const inputEl = item.querySelector('input');
    inputEl.oninput = () => {
      answersStore[fileKey][bid] = inputEl.value;
      const chip = document.getElementById('chip-' + bid);
      if(chip){
        chip.textContent = inputEl.value || bid;
        chip.className = 'blankchip ' + (inputEl.value ? 'pending' : 'empty');
      }
    };
  });
}

function isCorrect(bid, blanksMap, fileKey){
  const b = blanksMap[bid];
  const given = (answersStore[fileKey][bid] || '').trim();
  const expected = b.answer;
  if(b.lenientHex){
    return given.toLowerCase().replace(/^0x0*/,'0x') === expected.toLowerCase().replace(/^0x0*/,'0x');
  }
  return given === expected;
}

function checkAnswers(fileKey){
  const blanksMap = fileKey === 'linker' ? LINKER_BLANKS : STARTUP_BLANKS;
  let correctCount = 0;
  Object.keys(blanksMap).forEach(bid=>{
    const ok = isCorrect(bid, blanksMap, fileKey);
    const chip = document.getElementById('chip-' + bid);
    const inputEl = document.getElementById('input-' + bid);
    if(chip){ chip.className = 'blankchip ' + (ok ? 'correct' : (answersStore[fileKey][bid] ? 'wrong' : 'empty')); }
    if(inputEl){ inputEl.className = ok ? 'correct' : (answersStore[fileKey][bid] ? 'wrong' : ''); }
    if(ok) correctCount++;
  });
  const total = Object.keys(blanksMap).length;
  const status = document.getElementById('status-' + fileKey);
  status.textContent = `${correctCount} / ${total} correct`;
  status.className = 'status ' + (correctCount === total ? 'ok' : 'bad');
  updateBadge(fileKey);
  updateGenerateButton();
}

function revealAll(fileKey){
  const blanksMap = fileKey === 'linker' ? LINKER_BLANKS : STARTUP_BLANKS;
  Object.keys(blanksMap).forEach(bid=>{
    answersStore[fileKey][bid] = blanksMap[bid].answer;
    const inputEl = document.getElementById('input-' + bid);
    if(inputEl) inputEl.value = blanksMap[bid].answer;
  });
  renderCode(fileKey, fileKey === 'linker' ? LINKER_TEMPLATE : STARTUP_TEMPLATE, blanksMap);
  checkAnswers(fileKey);
}

function updateBadge(fileKey){
  const blanksMap = fileKey === 'linker' ? LINKER_BLANKS : STARTUP_BLANKS;
  const total = Object.keys(blanksMap).length;
  const correct = Object.keys(blanksMap).filter(bid=>isCorrect(bid, blanksMap, fileKey)).length;
  document.getElementById(fileKey + 'Badge').textContent = `(${correct}/${total})`;
}

function allComplete(){
  const lOk = Object.keys(LINKER_BLANKS).every(bid=>isCorrect(bid, LINKER_BLANKS, 'linker'));
  const sOk = Object.keys(STARTUP_BLANKS).every(bid=>isCorrect(bid, STARTUP_BLANKS, 'startup'));
  return lOk && sOk;
}
function updateGenerateButton(){
  const btn = document.getElementById('genBtn');
  const status = document.getElementById('genStatus');
  if(allComplete()){
    btn.disabled = false;
    status.textContent = 'Everything checks out — generate your complete files below.';
    status.className = 'status ok';
  } else {
    btn.disabled = true;
    status.textContent = 'Complete both files above with all-correct answers to unlock this.';
    status.className = 'status';
  }
}

function fillTemplate(template, blanksMap, fileKey){
  let out = template;
  Object.keys(blanksMap).forEach(bid=>{
    out = out.replace('{{' + bid + '}}', answersStore[fileKey][bid] || blanksMap[bid].answer);
  });
  return out;
}

function generateFiles(){
  if(!allComplete()) return;
  document.getElementById('finalLinker').textContent = fillTemplate(LINKER_TEMPLATE, LINKER_BLANKS, 'linker');
  document.getElementById('finalStartup').textContent = fillTemplate(STARTUP_TEMPLATE, STARTUP_BLANKS, 'startup');
  document.getElementById('generatedBox').classList.add('show');
  document.getElementById('generatedBox').scrollIntoView({behavior:'smooth', block:'start'});
}

function copyText(elId){
  const text = document.getElementById(elId).textContent;
  if(navigator.clipboard && navigator.clipboard.writeText){ navigator.clipboard.writeText(text).catch(()=>{}); }
}

/* ============================================================
   TABS
============================================================ */
function switchTab(name){
  document.getElementById('tabLinker').classList.toggle('active', name==='linker');
  document.getElementById('tabStartup').classList.toggle('active', name==='startup');
  document.getElementById('wrap-linker').classList.toggle('active', name==='linker');
  document.getElementById('wrap-startup').classList.toggle('active', name==='startup');
}

/* ============================================================
   INIT
============================================================ */
renderCode('linker', LINKER_TEMPLATE, LINKER_BLANKS);
renderQuestionnaire('linker', LINKER_BLANKS);
renderCode('startup', STARTUP_TEMPLATE, STARTUP_BLANKS);
renderQuestionnaire('startup', STARTUP_BLANKS);
updateBadge('linker');
updateBadge('startup');
updateGenerateButton();
</script>
</body>
</html>
Uploading complete_the_files_lab.html…]()

## END 

======================================================
## Start

## Interactive Task Lab

[Interactive_Task_Lab.html](https://github.com/user-attachments/files/32473172/Interactive_Task_Lab.html)





<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Interactive Task Lab — Toolchain, Porting &amp; Driver Development</title>
<style>
  :root{
    --navy:#16213E; --navy-deep:#0C1226; --navy-soft:#22335C; --navy-tint:#EEF1F7;
    --cyan:#17B9CC; --cyan-dark:#0A7F91; --cyan-tint:#E7F7F9;
    --amber:#FFA630; --amber-dark:#B96A00; --amber-tint:#FFEFDA;
    --white:#FFFFFF; --line:#DCE6F0; --muted:#5B6B8C; --text:#16213E;
    --error:#E2574C; --error-tint:#FDEBEA;
    --radius:14px; --radius-sm:9px;
    --shadow:0 10px 30px -12px rgba(12,18,38,.18);
    --shadow-sm:0 4px 14px -6px rgba(12,18,38,.14);
    --mono:'Courier New', ui-monospace, SFMono-Regular, Consolas, monospace;
    --sans:-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
  }
  *{box-sizing:border-box;}
  html{scroll-behavior:smooth;}
  body{
    margin:0; font-family:var(--sans); color:var(--text); background:var(--white);
    -webkit-font-smoothing:antialiased;
  }
  h1,h2,h3{margin:0; font-family:var(--sans);}
  p{margin:0;}
  button{font-family:inherit; cursor:pointer;}
  .wrap{max-width:960px; margin:0 auto; padding:0 24px;}

  /* ---------- NAV ---------- */
  #topnav{
    position:sticky; top:0; z-index:50; background:rgba(12,18,38,.96);
    backdrop-filter:blur(6px); border-bottom:1px solid rgba(255,255,255,.08);
  }
  .nav-inner{max-width:1080px; margin:0 auto; padding:10px 20px; display:flex; align-items:center; gap:14px;}
  .nav-brand{display:flex; align-items:center; gap:8px; color:#fff; font-weight:700; font-size:13.5px; white-space:nowrap;}
  .nav-chip{width:24px; height:24px; border-radius:7px; background:var(--cyan); display:flex; align-items:center; justify-content:center; font-size:13px;}
  .nav-pills{display:flex; gap:6px; flex-wrap:wrap; flex:1;}
  .nav-pill{
    display:flex; align-items:center; gap:6px; padding:6px 11px; border-radius:20px;
    background:rgba(255,255,255,.06); color:#B9C6DE; text-decoration:none; font-size:12px; font-weight:600;
    border:1px solid transparent; transition:background .2s, color .2s, border-color .2s;
  }
  .nav-pill:hover{background:rgba(255,255,255,.12); color:#fff;}
  .nav-dot{width:7px; height:7px; border-radius:50%; background:#3A4A70; transition:background .25s, box-shadow .25s;}
  .nav-pill-done .nav-dot{background:var(--cyan); box-shadow:0 0 6px var(--cyan);}
  .nav-pill-done{color:#fff; border-color:rgba(23,185,204,.35);}
  #progress-badge{
    background:var(--amber); color:var(--navy-deep); font-weight:800; font-size:12.5px;
    padding:6px 12px; border-radius:20px; white-space:nowrap;
  }

  /* ---------- HERO ---------- */
  #hero{background:var(--navy-deep); color:#fff; padding:56px 0 46px; text-align:center; position:relative; overflow:hidden;}
  #hero::before{
    content:''; position:absolute; left:-120px; bottom:-160px; width:340px; height:340px; border-radius:50%;
    background:radial-gradient(circle, rgba(23,185,204,.20), transparent 70%);
  }
  #hero::after{
    content:''; position:absolute; right:-120px; top:-160px; width:340px; height:340px; border-radius:50%;
    background:radial-gradient(circle, rgba(255,166,48,.14), transparent 70%);
  }
  .kicker{
    color:var(--cyan); font-weight:700; font-size:12.5px; letter-spacing:2.5px; text-transform:uppercase;
  }
  #hero h1{font-size:clamp(28px,4.6vw,42px); font-weight:800; margin:12px 0 10px; letter-spacing:-.02em;}
  #hero .sub{color:#C7D2E8; font-size:15.5px; max-width:560px; margin:0 auto; line-height:1.55; position:relative;}
  .circuit-track{position:relative; max-width:640px; margin:38px auto 6px; padding:0 20px;}
  .circuit-line{position:absolute; left:20px; right:20px; top:17px; height:2px; background:#2A3B5C; z-index:0;}
  .circuit-nodes{position:relative; z-index:1; display:flex; justify-content:space-between;}
  .led-dot{
    width:15px; height:15px; border-radius:50%; background:var(--navy-soft); border:2px solid #3A4A70;
    transition:background .3s, border-color .3s, box-shadow .3s, transform .3s;
  }
  .led-dot.led-lit{background:var(--cyan); border-color:var(--cyan); box-shadow:0 0 12px 2px rgba(23,185,204,.7); transform:scale(1.15);}
  .hero-hint{margin-top:14px; font-size:12.5px; color:#8592B0;}

  /* ---------- SECTIONS ---------- */
  .task-section{
    padding:52px 0; border-bottom:1px solid var(--line);
    opacity:0; transform:translateY(22px); transition:opacity .6s ease, transform .6s ease;
  }
  .task-section.section-visible{opacity:1; transform:translateY(0);}
  .task-head{margin-bottom:22px;}
  .task-kicker{display:flex; align-items:center; gap:8px; color:var(--cyan-dark); font-weight:700; font-size:12px; letter-spacing:2px; text-transform:uppercase; margin-bottom:8px;}
  .task-badge-icon{width:20px; height:20px; border-radius:6px; background:var(--amber); color:#fff; display:flex; align-items:center; justify-content:center; font-size:11px;}
  .task-title{font-size:clamp(20px,3vw,26px); font-weight:800; color:var(--navy); letter-spacing:-.01em;}
  .task-intro{color:var(--muted); font-size:14.5px; margin-top:8px; max-width:680px; line-height:1.55;}
  .analogy-box{
    background:var(--cyan-tint); border-radius:var(--radius); padding:18px 20px; margin:18px 0 22px;
    font-size:14px; line-height:1.6; color:var(--text);
  }
  .analogy-box b{color:var(--navy);}
  .widget{background:var(--white); border:1px solid var(--line); border-radius:var(--radius); padding:22px; box-shadow:var(--shadow-sm);}
  .why-note{margin-top:16px; font-size:12.5px; color:var(--muted); font-style:italic;}

  .btn{
    border:none; border-radius:9px; padding:10px 18px; font-weight:700; font-size:13.5px;
    transition:transform .15s, box-shadow .15s, background .15s; display:inline-flex; align-items:center; gap:6px;
  }
  .btn:active{transform:scale(.97);}
  .btn-primary{background:var(--navy); color:#fff;}
  .btn-primary:hover{background:var(--navy-soft);}
  .btn-ghost{background:var(--cyan-tint); color:var(--cyan-dark);}
  .btn-ghost:hover{background:#d7f0f3;}
  .btn:disabled{opacity:.45; cursor:not-allowed;}

  .feedback{margin-top:14px; padding:11px 15px; border-radius:9px; font-size:13.5px; font-weight:600; display:none;}
  .feedback-success{display:block; background:var(--cyan-tint); color:var(--cyan-dark);}
  .feedback-error{display:block; background:var(--error-tint); color:var(--error);}

  @keyframes shake{
    10%,90%{transform:translateX(-1px);} 20%,80%{transform:translateX(2px);}
    30%,50%,70%{transform:translateX(-4px);} 40%,60%{transform:translateX(4px);}
  }
  .tile-shake{animation:shake .5s;}
  @keyframes pop{0%{transform:scale(1);} 45%{transform:scale(1.05);} 100%{transform:scale(1);}}
  .tile-correct{animation:pop .4s;}

  /* ---- Task 1 & 3b: order tiles ---- */
  .tile-row{display:flex; gap:12px; flex-wrap:wrap; margin-bottom:16px;}
  .tile{
    flex:1 1 130px; min-width:130px; background:var(--white); border:2px solid var(--line); border-radius:var(--radius-sm);
    padding:14px 12px 12px; text-align:center; position:relative; transition:border-color .25s, background .25s;
  }
  .tile-pos{
    position:absolute; top:-10px; left:50%; transform:translateX(-50%); width:22px; height:22px; border-radius:50%;
    background:var(--navy); color:#fff; font-size:11.5px; font-weight:800; display:flex; align-items:center; justify-content:center;
  }
  .tile-label{font-weight:700; font-size:13.5px; color:var(--navy); margin:8px 0 10px;}
  .tile-controls{display:flex; justify-content:center; gap:6px;}
  .tile-btn{
    width:30px; height:30px; border-radius:7px; border:1px solid var(--line); background:var(--cyan-tint);
    color:var(--cyan-dark); font-size:13px; font-weight:700;
  }
  .tile-btn:disabled{opacity:.3; cursor:not-allowed;}
  .tile-reveal{font-size:11px; color:var(--amber-dark); font-weight:700; margin-top:8px; min-height:14px;}
  .tile.tile-correct-state{border-color:var(--cyan); background:var(--cyan-tint);}

  /* ---- Task 2 & 7: matching ---- */
  .match-grid{display:grid; grid-template-columns:1fr 1fr; gap:26px;}
  @media(max-width:620px){.match-grid{grid-template-columns:1fr;}}
  .match-col{display:flex; flex-direction:column; gap:9px;}
  .match-item{
    text-align:left; width:100%; padding:12px 14px; border-radius:9px; border:1.5px solid var(--line);
    background:var(--white); font-size:13.5px; color:var(--text); font-weight:600; transition:all .2s;
  }
  .match-item:hover:not(:disabled){border-color:var(--cyan);}
  .match-selected{border-color:var(--amber); background:var(--amber-tint);}
  .match-done{background:var(--cyan-tint); border-color:var(--cyan); color:var(--cyan-dark); opacity:.85;}
  .match-wrong{border-color:var(--error) !important; background:var(--error-tint) !important; animation:shake .5s;}

  /* ---- Task 3a & 4: bins ---- */
  .bin-pool{display:flex; gap:10px; flex-wrap:wrap; min-height:44px; margin-bottom:20px; padding:12px; background:var(--navy-tint,#EEF1F7); border-radius:9px;}
  .bin-chip{
    padding:9px 13px; border-radius:20px; border:1.5px solid var(--line); background:#fff; font-size:12.5px;
    font-weight:600; color:var(--text);
  }
  .bin-chip-selected{border-color:var(--amber); background:var(--amber-tint);}
  .bin-row{display:grid; grid-template-columns:1fr 1fr; gap:16px;}
  @media(max-width:620px){.bin-row{grid-template-columns:1fr;}}
  .bin-drop{border:2px dashed var(--line); border-radius:var(--radius-sm); padding:14px; min-height:150px; cursor:pointer; transition:border-color .2s, background .2s;}
  .bin-drop:hover{border-color:var(--cyan);}
  .bin-drop:focus-visible{outline:2.5px solid var(--amber); outline-offset:2px;}
  .bin-wrong{border-color:var(--error) !important; background:var(--error-tint);}
  .bin-title{font-weight:800; font-size:12.5px; text-transform:uppercase; letter-spacing:.5px; margin-bottom:10px; display:flex; align-items:center; gap:6px;}
  .bin-title-same{color:var(--cyan-dark);}
  .bin-title-change{color:var(--navy);}
  .bin-list{display:flex; flex-direction:column; gap:7px;}
  .bin-chip-placed{
    padding:8px 12px; border-radius:7px; background:var(--cyan-tint); font-size:12.5px; font-weight:600;
    color:var(--navy); display:flex; justify-content:space-between; gap:8px;
  }
  .chip-check{color:var(--cyan-dark); font-weight:800;}

  /* ---- Task 5: GPIO switches ---- */
  .switch-row{display:flex; gap:10px; justify-content:center; margin:20px 0 6px; flex-wrap:wrap;}
  .gpio-switch{
    width:52px; height:80px; border-radius:10px; border:2px solid var(--line); background:#fff;
    display:flex; flex-direction:column; align-items:center; justify-content:flex-end; padding-bottom:8px;
    position:relative; transition:border-color .2s, background .25s;
  }
  .gpio-switch .switch-knob{
    width:34px; height:34px; border-radius:8px; background:var(--muted); margin-bottom:8px;
    transition:background .25s, transform .25s;
  }
  .gpio-switch.switch-on{border-color:var(--cyan); background:var(--cyan-tint);}
  .gpio-switch.switch-on .switch-knob{background:var(--cyan-dark); transform:translateY(-30px);}
  .switch-bitnum{font-size:11px; font-weight:800; color:var(--muted); font-family:var(--mono);}
  .gpio-switch.switch-on .switch-bitnum{color:var(--cyan-dark);}
  .readout-row{display:flex; gap:14px; justify-content:center; margin:22px 0; flex-wrap:wrap;}
  .readout-card{background:var(--navy-deep); color:#fff; border-radius:11px; padding:14px 22px; text-align:center; min-width:150px;}
  .readout-label{font-size:10.5px; color:#8592B0; text-transform:uppercase; letter-spacing:1.5px; font-weight:700;}
  .readout-value{font-family:var(--mono); font-size:22px; font-weight:700; color:var(--cyan); margin-top:4px; letter-spacing:2px;}
  .challenge-box{background:var(--amber-tint); border-radius:9px; padding:13px 16px; font-size:13.5px; font-weight:700; color:var(--amber-dark); text-align:center; margin-bottom:16px;}
  .challenge-actions{display:flex; justify-content:center; gap:10px;}

  /* ---- Task 6: h vs c ---- */
  .hvc-grid{display:grid; grid-template-columns:1fr 1fr; gap:24px;}
  @media(max-width:700px){.hvc-grid{grid-template-columns:1fr;}}
  .field-label{font-size:12px; font-weight:700; color:var(--navy); margin-bottom:6px; display:block;}
  .text-input{
    width:100%; padding:10px 12px; border:1.5px solid var(--line); border-radius:8px; font-size:13.5px;
    margin-bottom:10px; font-family:var(--sans); color:var(--text);
  }
  .text-input:focus{outline:none; border-color:var(--cyan);}
  .preview-card{background:var(--navy-tint,#EEF1F7); border-radius:11px; padding:16px; margin-top:6px;}
  .preview-label{font-size:10.5px; font-weight:800; text-transform:uppercase; letter-spacing:1px; color:var(--muted); margin-bottom:8px;}
  .menu-preview{font-family:'Courier New',monospace; font-size:16px; font-weight:700; color:var(--navy); padding:10px 0;}
  .ticket-preview{margin:0; padding-left:20px; font-size:13px; color:var(--navy); line-height:1.9;}
  .ticket-placeholder{color:var(--muted); font-style:italic; list-style:none; margin-left:-20px;}
  .example-box{max-height:0; overflow:hidden; transition:max-height .35s ease; font-size:13px; color:var(--muted); background:#fff; border-radius:8px;}
  .example-box.example-visible{max-height:200px; margin-top:12px; padding:12px 14px; border:1px dashed var(--line);}

  /* ---- confetti ---- */
  .confetti-piece{position:fixed; width:8px; height:8px; pointer-events:none; z-index:999; animation:confetti-fall .9s ease-out forwards;}
  @keyframes confetti-fall{to{transform:translate(var(--dx),var(--dy)) rotate(var(--rot)); opacity:0;}}

  /* ---- completion banner ---- */
  #completion-banner{
    display:none; background:linear-gradient(135deg,var(--navy-deep),var(--navy)); color:#fff; text-align:center;
    padding:44px 24px; margin-top:0;
  }
  #completion-banner.banner-visible{display:block;}
  #completion-banner h2{font-size:26px; margin-bottom:8px;}
  #completion-banner p{color:#C7D2E8; font-size:14px; max-width:480px; margin:0 auto;}

  footer{background:var(--navy-deep); color:#8592B0; text-align:center; padding:22px; font-size:12px;}

  @media(prefers-reduced-motion:reduce){
    .task-section{transition:none; opacity:1; transform:none;}
    .confetti-piece{display:none;}
    *{animation-duration:.01ms !important;}
  }
  @media(max-width:640px){
    .nav-pills{display:none;}
    .nav-inner{justify-content:space-between;}
  }
</style>
</head>
<body>

<nav id="topnav">
  <div class="nav-inner">
    <div class="nav-brand"><span class="nav-chip">⚙</span> Task Lab</div>
    <div class="nav-pills">
      <a class="nav-pill" data-section="build-process" href="#build-process"><span class="nav-dot"></span>Build Process</a>
      <a class="nav-pill" data-section="toolchain" href="#toolchain"><span class="nav-dot"></span>Toolchain</a>
      <a class="nav-pill" data-section="strive-porting" href="#strive-porting"><span class="nav-dot"></span>Strive &amp; Porting</a>
      <a class="nav-pill" data-section="layered" href="#layered"><span class="nav-dot"></span>Layers</a>
      <a class="nav-pill" data-section="gpio" href="#gpio"><span class="nav-dot"></span>GPIO</a>
      <a class="nav-pill" data-section="hvc" href="#hvc"><span class="nav-dot"></span>.h vs .c</a>
      <a class="nav-pill" data-section="interfaces" href="#interfaces"><span class="nav-dot"></span>Interfaces</a>
    </div>
    <div id="progress-badge"><span id="progress-count">0</span> / 7</div>
  </div>
</nav>

<header id="hero">
  <div class="wrap">
    <div class="kicker">NECOP Embedded Systems Training</div>
    <h1>Interactive Task Lab</h1>
    <p class="sub">Hands-on companion to <strong>Toolchain, Porting &amp; Driver Development</strong>. Play through all seven activities to power up the circuit below.</p>
    <div class="circuit-track">
      <div class="circuit-line"></div>
      <div class="circuit-nodes">
        <div class="led-dot" data-section="build-process"></div>
        <div class="led-dot" data-section="toolchain"></div>
        <div class="led-dot" data-section="strive-porting"></div>
        <div class="led-dot" data-section="layered"></div>
        <div class="led-dot" data-section="gpio"></div>
        <div class="led-dot" data-section="hvc"></div>
        <div class="led-dot" data-section="interfaces"></div>
      </div>
    </div>
    <div class="hero-hint">⚡ Complete all 7 tasks to light up the whole board</div>
  </div>
</header>

<main class="wrap">

  <!-- ============ TASK 1: BUILD PROCESS ============ -->
  <section class="task-section" id="build-process">
    <div class="task-head">
      <div class="task-kicker"><span class="task-badge-icon">🎓</span>Beginner Task · Build Process</div>
      <h2 class="task-title">Try It Yourself — The Recipe Translator</h2>
      <p class="task-intro">Think of building firmware like translating a recipe for a friend who speaks another language.</p>
    </div>
    <div class="analogy-box">
      <b>Source Code</b> = the recipe in your own language &nbsp;→&nbsp; <b>Compiler</b> = a translator rewrites it &nbsp;→&nbsp;
      <b>Assembler</b> = turned into a shorthand code &nbsp;→&nbsp; <b>Linker</b> = bound with borrowed recipes into one final cookbook.
    </div>
    <div class="widget" id="w-build">
      <div class="tile-row"></div>
      <button class="btn btn-primary check-btn" type="button">Check My Order</button>
      <div class="feedback"></div>
    </div>
    <p class="why-note">Why it matters: once you can name the 4 stages, every confusing build error starts to make sense.</p>
  </section>

  <!-- ============ TASK 2: TOOLCHAIN MATCHING ============ -->
  <section class="task-section" id="toolchain">
    <div class="task-head">
      <div class="task-kicker"><span class="task-badge-icon">🎓</span>Beginner Task · Toolchain</div>
      <h2 class="task-title">Try It Yourself — Match the Tool to the Job</h2>
      <p class="task-intro">Click a tool on the left, then click the job it performs on the right.</p>
    </div>
    <div class="widget" id="w-toolchain">
      <div class="match-grid">
        <div class="match-col match-left"></div>
        <div class="match-col match-right"></div>
      </div>
      <div class="feedback"></div>
    </div>
  </section>

  <!-- ============ TASK 3: STRIVE IDE & PORTING ============ -->
  <section class="task-section" id="strive-porting">
    <div class="task-head">
      <div class="task-kicker"><span class="task-badge-icon">🎓</span>Beginner Task · Strive IDE &amp; Porting</div>
      <h2 class="task-title">Try It Yourself — Same Game, New Console</h2>
      <p class="task-intro">Porting firmware is like playing your favourite video game on a new console — the story and rules stay the same, but the controller layout might change.</p>
    </div>

    <h3 style="font-size:14px; color:var(--navy); margin:22px 0 10px;">Part A — Sort: Stays the Same or Changes?</h3>
    <div class="widget" id="w-porting" style="margin-bottom:26px;">
      <div class="bin-pool"></div>
      <div class="bin-row">
        <div class="bin-drop" data-bin="same" tabindex="0" role="button" aria-label="Place in Stays the Same">
          <div class="bin-title bin-title-same">✓ Stays the Same</div>
          <div class="bin-list"></div>
        </div>
        <div class="bin-drop" data-bin="change" tabindex="0" role="button" aria-label="Place in Changes">
          <div class="bin-title bin-title-change">⚙ Changes</div>
          <div class="bin-list"></div>
        </div>
      </div>
      <div class="feedback"></div>
    </div>

    <h3 style="font-size:14px; color:var(--navy); margin:22px 0 10px;">Part B — Put the 6 Strive IDE Steps in Order</h3>
    <div class="widget" id="w-strive">
      <div class="tile-row"></div>
      <button class="btn btn-primary check-btn" type="button">Check My Order</button>
      <div class="feedback"></div>
    </div>
  </section>

  <!-- ============ TASK 4: LAYERED ARCHITECTURE ============ -->
  <section class="task-section" id="layered">
    <div class="task-head">
      <div class="task-kicker"><span class="task-badge-icon">🎓</span>Beginner Task · Layered Architecture</div>
      <h2 class="task-title">Try It Yourself — Press the Pedal, Not the Engine</h2>
      <p class="task-intro">Sort each item into what you actually SEE (the simple API) or what's HIDDEN underneath (the implementation).</p>
    </div>
    <div class="widget" id="w-layered">
      <div class="bin-pool"></div>
      <div class="bin-row">
        <div class="bin-drop" data-bin="see" tabindex="0" role="button" aria-label="Place in What You See">
          <div class="bin-title bin-title-same">👁 What You See (API)</div>
          <div class="bin-list"></div>
        </div>
        <div class="bin-drop" data-bin="hidden" tabindex="0" role="button" aria-label="Place in What's Hidden">
          <div class="bin-title bin-title-change">🔧 What's Hidden (Implementation)</div>
          <div class="bin-list"></div>
        </div>
      </div>
      <div class="feedback"></div>
    </div>
    <p class="why-note">Why it matters: this is the exact same reason main.c never touches GPIOx-&gt;ODR directly.</p>
  </section>

  <!-- ============ TASK 5: GPIO REGISTERS ============ -->
  <section class="task-section" id="gpio">
    <div class="task-head">
      <div class="task-kicker"><span class="task-badge-icon">🎓</span>Beginner Task · GPIO Registers</div>
      <h2 class="task-title">Try It Yourself — 8 Light Switches in a Row</h2>
      <p class="task-intro">Click the switches to turn them ON (1) or OFF (0). Watch the binary and decimal readouts update live.</p>
    </div>
    <div class="widget" id="w-gpio">
      <div class="switch-row"></div>
      <div class="readout-row">
        <div class="readout-card"><div class="readout-label">Binary</div><div class="readout-value binary-readout">00000000</div></div>
        <div class="readout-card"><div class="readout-label">Decimal</div><div class="readout-value decimal-readout">0</div></div>
      </div>
      <div class="challenge-box challenge-desc">Challenge 1 of 2: Turn ON switch 3 only.</div>
      <div class="challenge-actions">
        <button class="btn btn-primary check-btn" type="button">Check Challenge</button>
      </div>
      <div class="feedback"></div>
    </div>
  </section>

  <!-- ============ TASK 6: .h vs .c ============ -->
  <section class="task-section" id="hvc">
    <div class="task-head">
      <div class="task-kicker"><span class="task-badge-icon">🎓</span>Beginner Task · .h vs .c Files</div>
      <h2 class="task-title">Try It Yourself — The Menu and The Kitchen</h2>
      <p class="task-intro">A restaurant MENU (.h) lists what you can order. The KITCHEN (.c) holds the real steps, hidden from the customer. Write your own!</p>
    </div>
    <div class="widget" id="w-hvc">
      <div class="hvc-grid">
        <div>
          <label class="field-label">Your favourite dish (the .h "menu")</label>
          <input class="text-input dish-input" type="text" placeholder="e.g. Chicken Biryani" maxlength="60">
          <label class="field-label">3 kitchen steps (the .c "implementation")</label>
          <input class="text-input step-input" type="text" placeholder="Step 1…" maxlength="80">
          <input class="text-input step-input" type="text" placeholder="Step 2…" maxlength="80">
          <input class="text-input step-input" type="text" placeholder="Step 3…" maxlength="80">
          <button class="btn btn-ghost reveal-btn" type="button">Reveal Example</button>
          <div class="example-box">
            <b>gpio.h (menu):</b> "Biryani"<br>
            <b>gpio.c (kitchen):</b> 1) Marinate chicken &nbsp;2) Layer with rice &amp; spices &nbsp;3) Slow-cook on dum for 25 min
          </div>
        </div>
        <div>
          <div class="preview-card">
            <div class="preview-label">📋 gpio.h — the menu</div>
            <div class="menu-preview">Your dish name here…</div>
          </div>
          <div class="preview-card" style="margin-top:14px;">
            <div class="preview-label">🍳 gpio.c — the kitchen ticket</div>
            <ol class="ticket-preview"><li class="ticket-placeholder">Your steps will appear here…</li></ol>
          </div>
        </div>
      </div>
      <button class="btn btn-primary done-btn" type="button" style="margin-top:16px;">Mark as Done</button>
      <div class="feedback"></div>
    </div>
  </section>

  <!-- ============ TASK 7: PERIPHERAL INTERFACES ============ -->
  <section class="task-section" id="interfaces">
    <div class="task-head">
      <div class="task-kicker"><span class="task-badge-icon">🎓</span>Beginner Task · Peripheral Interfaces</div>
      <h2 class="task-title">Try It Yourself — Everyday Communication</h2>
      <p class="task-intro">Match each interface to its everyday twin.</p>
    </div>
    <div class="widget" id="w-interfaces">
      <div class="match-grid">
        <div class="match-col match-left"></div>
        <div class="match-col match-right"></div>
      </div>
      <div class="feedback"></div>
    </div>
  </section>

</main>

<div id="completion-banner">
  <h2>⚡ Circuit Complete!</h2>
  <p>You've finished all 7 tasks — from build pipeline to peripheral interfaces. That's a full pass through the whole embedded toolchain, hands-on.</p>
</div>

<footer>Toolchain, Porting &amp; Driver Development — NECOP Embedded Systems Training · Interactive Task Lab</footer>

<script>
(function(){
  "use strict";

  /* ---------------- shared utilities ---------------- */
  function shuffle(arr){
    var a = arr.slice();
    for (var i = a.length - 1; i > 0; i--){
      var j = Math.floor(Math.random() * (i + 1));
      var t = a[i]; a[i] = a[j]; a[j] = t;
    }
    return a;
  }
  function arraysEqual(a,b){
    return a.length === b.length && a.every(function(v,i){ return v === b[i]; });
  }
  function escapeHtml(str){
    var d = document.createElement('div');
    d.textContent = str;
    return d.innerHTML;
  }
  function celebrate(container){
    try{
      var rect = container.getBoundingClientRect();
      spawnConfetti(rect.left + rect.width/2, rect.top + 30, 20);
    }catch(e){}
  }
  function spawnConfetti(x, y, count){
    var colors = ['#17B9CC','#FFA630','#16213E','#0A7F91'];
    for (var i=0;i<count;i++){
      var p = document.createElement('div');
      p.className = 'confetti-piece';
      p.style.left = x + 'px';
      p.style.top = y + 'px';
      p.style.background = colors[i % colors.length];
      var dx = (Math.random()-0.5) * 240;
      var dy = 110 + Math.random()*170;
      var rot = (Math.random()-0.5)*720;
      p.style.setProperty('--dx', dx+'px');
      p.style.setProperty('--dy', dy+'px');
      p.style.setProperty('--rot', rot+'deg');
      document.body.appendChild(p);
      (function(el){ setTimeout(function(){ el.remove(); }, 950); })(p);
    }
  }

  /* ---------------- progress tracking ---------------- */
  var TOTAL_SECTIONS = 7;
  var completed = {};
  function markSectionComplete(id){
    if (completed[id]) return;
    completed[id] = true;
    var count = Object.keys(completed).length;
    var countEl = document.getElementById('progress-count');
    if (countEl) countEl.textContent = count;
    document.querySelectorAll('.led-dot[data-section="'+id+'"]').forEach(function(el){ el.classList.add('led-lit'); });
    document.querySelectorAll('.nav-pill[data-section="'+id+'"]').forEach(function(el){ el.classList.add('nav-pill-done'); });
    if (count === TOTAL_SECTIONS){
      var banner = document.getElementById('completion-banner');
      if (banner){ banner.classList.add('banner-visible'); }
      spawnConfetti(window.innerWidth/2, 80, 70);
    }
  }

  /* ---------------- Task 1 & 3b: order tasks ---------------- */
  function initOrderTask(widgetId, items, correctOrder, revealLabels, onComplete){
    var root = document.getElementById(widgetId);
    if (!root) return;
    var tileRow = root.querySelector('.tile-row');
    var checkBtn = root.querySelector('.check-btn');
    var feedback = root.querySelector('.feedback');
    var current = shuffle(items.map(function(i){ return i.key; }));
    var tries = 0;
    while (arraysEqual(current, correctOrder) && tries < 12){
      current = shuffle(items.map(function(i){ return i.key; }));
      tries++;
    }

    function itemFor(key){ return items.filter(function(i){ return i.key === key; })[0]; }

    function render(){
      tileRow.innerHTML = current.map(function(key, idx){
        var item = itemFor(key);
        var leftDisabled = idx === 0 ? 'disabled' : '';
        var rightDisabled = idx === current.length - 1 ? 'disabled' : '';
        return '<div class="tile" data-key="' + key + '">' +
          '<div class="tile-pos">' + (idx+1) + '</div>' +
          '<div class="tile-label">' + escapeHtml(item.label) + '</div>' +
          '<div class="tile-controls">' +
            '<button type="button" class="tile-btn" data-action="left" data-key="' + key + '" ' + leftDisabled + ' aria-label="Move left">\u25C0</button>' +
            '<button type="button" class="tile-btn" data-action="right" data-key="' + key + '" ' + rightDisabled + ' aria-label="Move right">\u25B6</button>' +
          '</div>' +
          '<div class="tile-reveal"></div>' +
        '</div>';
      }).join('');
      tileRow.querySelectorAll('.tile-btn').forEach(function(btn){
        btn.addEventListener('click', function(){
          var key = btn.getAttribute('data-key');
          var dir = btn.getAttribute('data-action') === 'left' ? -1 : 1;
          var idx = current.indexOf(key);
          var newIdx = idx + dir;
          if (newIdx < 0 || newIdx >= current.length) return;
          var tmp = current[idx]; current[idx] = current[newIdx]; current[newIdx] = tmp;
          render();
        });
      });
    }
    render();

    checkBtn.addEventListener('click', function(){
      if (arraysEqual(current, correctOrder)){
        feedback.className = 'feedback feedback-success';
        feedback.textContent = '\u2713 Correct order! Nicely done.';
        tileRow.querySelectorAll('.tile').forEach(function(tileEl){
          tileEl.classList.add('tile-correct', 'tile-correct-state');
          var key = tileEl.getAttribute('data-key');
          var reveal = tileEl.querySelector('.tile-reveal');
          if (reveal && revealLabels && revealLabels[key]) reveal.textContent = revealLabels[key];
        });
        checkBtn.disabled = true;
        celebrate(root);
        onComplete();
      } else {
        feedback.className = 'feedback feedback-error';
        feedback.textContent = 'Not quite the right order yet — use the arrows to rearrange, then check again.';
        tileRow.querySelectorAll('.tile').forEach(function(t){
          t.classList.add('tile-shake');
          setTimeout(function(){ t.classList.remove('tile-shake'); }, 500);
        });
      }
    });
  }

  initOrderTask('w-build', [
    {key:'source', label:'Source Code'},
    {key:'compiler', label:'Compiler'},
    {key:'assembler', label:'Assembler'},
    {key:'linker', label:'Linker'}
  ], ['source','compiler','assembler','linker'], {
    source:'= Language', compiler:'= Words', assembler:'= Code', linker:'= Book'
  }, function(){ markSectionComplete('build-process'); });

  initOrderTask('w-strive', [
    {key:'create', label:'Create Project'},
    {key:'configure', label:'Configure'},
    {key:'write', label:'Write Code'},
    {key:'build', label:'Build'},
    {key:'flash', label:'Flash'},
    {key:'debug', label:'Debug'}
  ], ['create','configure','write','build','flash','debug'], null, function(){ striveDone = true; checkStrivePorting(); });

  /* ---------------- Task 2 & 7: matching ---------------- */
  function initMatchTask(widgetId, leftItems, rightMap, onComplete){
    var root = document.getElementById(widgetId);
    if (!root) return;
    var leftCol = root.querySelector('.match-left');
    var rightCol = root.querySelector('.match-right');
    var feedback = root.querySelector('.feedback');
    var rightItems = shuffle(Object.keys(rightMap).map(function(k){ return {key:k, label: rightMap[k]}; }));
    var selectedLeft = null;
    var matched = {};

    function render(){
      leftCol.innerHTML = leftItems.map(function(it){
        var done = !!matched[it.key];
        var sel = selectedLeft === it.key;
        return '<button type="button" class="match-item' + (done?' match-done':'') + (sel?' match-selected':'') +
          '" data-key="' + it.key + '" ' + (done?'disabled':'') + '>' + escapeHtml(it.label) + (done?' \u2713':'') + '</button>';
      }).join('');
      rightCol.innerHTML = rightItems.map(function(it){
        var done = !!matched[it.key];
        return '<button type="button" class="match-item' + (done?' match-done':'') +
          '" data-key="' + it.key + '" ' + (done?'disabled':'') + '>' + escapeHtml(it.label) + (done?' \u2713':'') + '</button>';
      }).join('');
      leftCol.querySelectorAll('.match-item').forEach(function(btn){
        btn.addEventListener('click', function(){ selectedLeft = btn.getAttribute('data-key'); render(); });
      });
      rightCol.querySelectorAll('.match-item').forEach(function(btn){
        btn.addEventListener('click', function(){ onRightClick(btn); });
      });
    }
    function onRightClick(btn){
      if (!selectedLeft) return;
      var rightKey = btn.getAttribute('data-key');
      if (rightKey === selectedLeft){
        matched[selectedLeft] = true;
        selectedLeft = null;
        render();
        if (Object.keys(matched).length === leftItems.length){
          feedback.className = 'feedback feedback-success';
          feedback.textContent = '\u2713 All matched! Great work.';
          celebrate(root);
          onComplete();
        }
      } else {
        var leftBtn = leftCol.querySelector('.match-item[data-key="' + selectedLeft + '"]');
        btn.classList.add('match-wrong');
        if (leftBtn) leftBtn.classList.add('match-wrong');
        setTimeout(function(){
          btn.classList.remove('match-wrong');
          if (leftBtn) leftBtn.classList.remove('match-wrong');
          selectedLeft = null;
          render();
        }, 500);
      }
    }
    render();
  }

  initMatchTask('w-toolchain', [
    {key:'compiler', label:'Compiler'},
    {key:'debugger', label:'Debugger'},
    {key:'programmer', label:'Programmer'},
    {key:'assembler', label:'Assembler'}
  ], {
    compiler: 'Turns C code into assembly language',
    debugger: 'Finds bugs by pausing the program mid-run',
    programmer: 'Copies the final file onto the chip',
    assembler: 'Turns assembly into 1s and 0s (machine code)'
  }, function(){ markSectionComplete('toolchain'); });

  initMatchTask('w-interfaces', [
    {key:'gpio', label:'GPIO'},
    {key:'uart', label:'UART'},
    {key:'i2c', label:'I2C'},
    {key:'spi', label:'SPI'}
  ], {
    gpio: 'A doorbell button \u2014 one wire, one job: ON or OFF.',
    uart: 'A walkie-talkie between two friends \u2014 only 2 people, no names needed.',
    i2c: 'A class group chat \u2014 many people share one line, but everyone has a name.',
    spi: 'A private hotline straight to one person \u2014 dedicated wires, super fast.'
  }, function(){ markSectionComplete('interfaces'); });

  /* ---------------- Task 3a & 4: bin sort ---------------- */
  function initBinTask(widgetId, items, onComplete){
    var root = document.getElementById(widgetId);
    if (!root) return;
    var poolEl = root.querySelector('.bin-pool');
    var bins = root.querySelectorAll('.bin-drop');
    var feedback = root.querySelector('.feedback');
    var pool = shuffle(items.map(function(i){ return i.key; }));
    var placed = {};
    var selected = null;

    function itemFor(key){ return items.filter(function(i){ return i.key === key; })[0]; }

    function render(){
      poolEl.innerHTML = pool.filter(function(k){ return !placed[k]; }).map(function(k){
        var item = itemFor(k);
        var sel = selected === k ? ' bin-chip-selected' : '';
        return '<button type="button" class="bin-chip' + sel + '" data-key="' + k + '">' + escapeHtml(item.label) + '</button>';
      }).join('') || '<span style="color:var(--muted); font-size:12.5px;">All items placed \u2014 nice work!</span>';

      poolEl.querySelectorAll('.bin-chip').forEach(function(btn){
        btn.addEventListener('click', function(){ selected = btn.getAttribute('data-key'); render(); });
      });
      bins.forEach(function(binEl){
        var binId = binEl.getAttribute('data-bin');
        var list = binEl.querySelector('.bin-list');
        var here = Object.keys(placed).filter(function(k){ return placed[k] === binId; });
        list.innerHTML = here.map(function(k){
          var item = itemFor(k);
          return '<div class="bin-chip-placed">' + escapeHtml(item.label) + '<span class="chip-check">\u2713</span></div>';
        }).join('');
      });
    }
    bins.forEach(function(binEl){
      binEl.addEventListener('click', function(e){
        if (e.target.closest('.bin-chip-placed')) return;
        attemptPlace(binEl);
      });
      binEl.addEventListener('keydown', function(e){
        if (e.key === 'Enter' || e.key === ' ' || e.key === 'Spacebar'){
          e.preventDefault();
          attemptPlace(binEl);
        }
      });
    });
    function attemptPlace(binEl){
      if (!selected) return;
      var item = itemFor(selected);
      var binId = binEl.getAttribute('data-bin');
      if (item.bin === binId){
        placed[selected] = binId;
        selected = null;
        render();
        if (Object.keys(placed).length === items.length){
          feedback.className = 'feedback feedback-success';
          feedback.textContent = '\u2713 All sorted correctly!';
          celebrate(root);
          onComplete();
        }
      } else {
        binEl.classList.add('bin-wrong');
        setTimeout(function(){ binEl.classList.remove('bin-wrong'); }, 450);
      }
    }
    render();
  }

  initBinTask('w-porting', [
    {key:'story', label:'The story & levels', bin:'same'},
    {key:'rules', label:'Core gameplay rules', bin:'same'},
    {key:'characters', label:'Character names & abilities', bin:'same'},
    {key:'buttonmap', label:"Which button makes you jump", bin:'change'},
    {key:'resolution', label:'Screen resolution & button layout', bin:'change'},
    {key:'savefile', label:'Save file format', bin:'change'}
  ], function(){ portingDone = true; checkStrivePorting(); });

  initBinTask('w-layered', [
    {key:'gpiocall', label:'gpio_write(LED_PIN, HIGH);', bin:'see'},
    {key:'odrwrite', label:'GPIOx->ODR |= (1 << pin);', bin:'hidden'},
    {key:'pressswitch', label:'Press the light switch', bin:'see'},
    {key:'contacts', label:'Metal contacts touching inside the switch', bin:'hidden'},
    {key:'pedal', label:"Press the car's accelerator pedal", bin:'see'},
    {key:'injectors', label:'Fuel injectors spraying into the engine', bin:'hidden'}
  ], function(){ markSectionComplete('layered'); });

  /* ---------------- combined section 3 gate ---------------- */
  var portingDone = false, striveDone = false;
  function checkStrivePorting(){
    if (portingDone && striveDone) markSectionComplete('strive-porting');
  }

  /* ---------------- Task 5: GPIO switches ---------------- */
  (function initGpio(){
    var root = document.getElementById('w-gpio');
    if (!root) return;
    var switchRow = root.querySelector('.switch-row');
    var binaryEl = root.querySelector('.binary-readout');
    var decimalEl = root.querySelector('.decimal-readout');
    var challengeDesc = root.querySelector('.challenge-desc');
    var checkBtn = root.querySelector('.check-btn');
    var feedback = root.querySelector('.feedback');
    var states = [false,false,false,false,false,false,false,false];
    var challenges = [
      {bit:3, desc:'Challenge 1 of 2: Turn ON switch 3 only.'},
      {bit:5, desc:'Challenge 2 of 2: Turn ON switch 5 only (same example as the walkthrough slide).'}
    ];
    var idx = 0;

    function binaryStr(){ return states.map(function(s){ return s ? '1' : '0'; }).join(''); }
    function decimalVal(){
      var v = 0;
      for (var i=0;i<8;i++){ if (states[i]) v += Math.pow(2, 7-i); }
      return v;
    }
    function render(){
      switchRow.innerHTML = states.map(function(s, i){
        var bit = 7 - i;
        return '<button type="button" class="gpio-switch' + (s?' switch-on':'') + '" data-index="' + i + '" aria-label="bit ' + bit + '">' +
          '<span class="switch-knob"></span><span class="switch-bitnum">' + bit + '</span></button>';
      }).join('');
      binaryEl.textContent = binaryStr();
      decimalEl.textContent = decimalVal();
      switchRow.querySelectorAll('.gpio-switch').forEach(function(btn){
        btn.addEventListener('click', function(){
          var i = parseInt(btn.getAttribute('data-index'), 10);
          states[i] = !states[i];
          render();
        });
      });
      if (challenges[idx]) challengeDesc.textContent = challenges[idx].desc;
    }
    render();

    checkBtn.addEventListener('click', function(){
      var chal = challenges[idx];
      if (!chal) return;
      var met = states.every(function(s,i){ return s === ((7-i) === chal.bit); });
      if (met){
        idx++;
        if (idx >= challenges.length){
          feedback.className = 'feedback feedback-success';
          feedback.textContent = '\u2713 All challenges complete! You can read and write GPIO registers now.';
          challengeDesc.textContent = 'All challenges complete \u2014 nice work!';
          checkBtn.disabled = true;
          celebrate(root);
          markSectionComplete('gpio');
        } else {
          feedback.className = 'feedback feedback-success';
          feedback.textContent = '\u2713 Correct! Next challenge unlocked.';
          render();
        }
      } else {
        feedback.className = 'feedback feedback-error';
        feedback.textContent = 'Not yet \u2014 check your switches against the challenge above and try again.';
        switchRow.querySelectorAll('.gpio-switch').forEach(function(el){
          el.classList.add('tile-shake');
          setTimeout(function(){ el.classList.remove('tile-shake'); }, 500);
        });
      }
    });
  })();

  /* ---------------- Task 6: .h vs .c ---------------- */
  (function initHvc(){
    var root = document.getElementById('w-hvc');
    if (!root) return;
    var dishInput = root.querySelector('.dish-input');
    var stepInputs = root.querySelectorAll('.step-input');
    var menuPreview = root.querySelector('.menu-preview');
    var ticketPreview = root.querySelector('.ticket-preview');
    var doneBtn = root.querySelector('.done-btn');
    var revealBtn = root.querySelector('.reveal-btn');
    var exampleBox = root.querySelector('.example-box');
    var feedback = root.querySelector('.feedback');

    function update(){
      menuPreview.textContent = dishInput.value.trim() || 'Your dish name here\u2026';
      var steps = Array.prototype.slice.call(stepInputs).map(function(i){ return i.value.trim(); }).filter(Boolean);
      if (steps.length){
        ticketPreview.innerHTML = steps.map(function(s){ return '<li>' + escapeHtml(s) + '</li>'; }).join('');
      } else {
        ticketPreview.innerHTML = '<li class="ticket-placeholder">Your steps will appear here\u2026</li>';
      }
    }
    dishInput.addEventListener('input', update);
    stepInputs.forEach(function(i){ i.addEventListener('input', update); });
    update();

    revealBtn.addEventListener('click', function(){
      var visible = exampleBox.classList.toggle('example-visible');
      revealBtn.textContent = visible ? 'Hide Example' : 'Reveal Example';
    });

    doneBtn.addEventListener('click', function(){
      var stepsFilled = Array.prototype.slice.call(stepInputs).filter(function(i){ return i.value.trim(); }).length;
      if (dishInput.value.trim() && stepsFilled >= 1){
        feedback.className = 'feedback feedback-success';
        feedback.textContent = '\u2713 Nice! You just wrote your own .h (menu) and .c (kitchen steps).';
        celebrate(root);
        markSectionComplete('hvc');
      } else {
        feedback.className = 'feedback feedback-error';
        feedback.textContent = 'Write a dish name and at least one step first.';
      }
    });
  })();

  /* ---------------- scroll reveal ---------------- */
  var sections = document.querySelectorAll('.task-section');
  if ('IntersectionObserver' in window){
    var observer = new IntersectionObserver(function(entries){
      entries.forEach(function(entry){
        if (entry.isIntersecting){
          entry.target.classList.add('section-visible');
          observer.unobserve(entry.target);
        }
      });
    }, {threshold:0.12});
    sections.forEach(function(s){ observer.observe(s); });
  } else {
    sections.forEach(function(s){ s.classList.add('section-visible'); });
  }

})();
</script>
</body>
</html>

 ## END

======================================================

## START 

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


## END 

======================================================

## START

## 2-HOUR LAB EXERCISE
Build Process, Toolchain, Porting, Linker Script & startup.S

[Uploading lab<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>2-Hour Lab — Build Process, Toolchain, Porting, Linker &amp; Startup</title>
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

header{padding:26px 24px 14px; max-width:980px; margin:0 auto;}
header .eyebrow{font-family:var(--code); font-size:12px; color:var(--teal); letter-spacing:1.5px; font-weight:700; margin-bottom:8px;}
header h1{font-size:24px; margin-bottom:10px;}
header p{color:var(--text-1); font-size:14px; max-width:760px; margin-bottom:6px;}
.timebox{display:inline-flex; align-items:center; gap:8px; background:var(--amber-dim); color:var(--amber); border:1px solid var(--amber); border-radius:20px; padding:6px 14px; font-family:var(--code); font-size:12px; font-weight:700; margin-top:10px;}

.namebar{
  max-width:980px; margin:14px auto 0; background:var(--bg-1); border:1px solid var(--border); border-radius:12px;
  padding:14px 18px; display:flex; gap:14px; flex-wrap:wrap; align-items:center;
}
.namebar label{font-size:12px; color:var(--text-2); margin-right:6px;}
.namebar input{background:var(--bg-2); border:1px solid var(--border-strong); border-radius:7px; padding:7px 10px; font-size:13px;}
.namebar .saved{font-size:11.5px; color:var(--green); font-family:var(--code); margin-left:auto;}

nav.jumpnav{max-width:980px; margin:14px auto 0; display:flex; gap:5px; flex-wrap:wrap; padding:0 2px;}
.jumpbtn{width:30px; height:30px; border-radius:7px; background:var(--bg-1); border:1px solid var(--border); font-family:var(--code); font-size:11px; font-weight:700; color:var(--text-2);}
.jumpbtn.answered{background:var(--teal-dim); border-color:var(--teal); color:var(--teal);}

main{max-width:980px; margin:0 auto; padding:20px 24px 60px;}

.task{background:var(--bg-1); border:1px solid var(--border); border-radius:14px; padding:22px 24px; margin-bottom:18px; scroll-margin-top:16px;}
.task .taskhead{display:flex; align-items:center; gap:10px; margin-bottom:10px; flex-wrap:wrap;}
.tasknum{font-family:var(--code); font-weight:800; font-size:13px; color:var(--teal); background:var(--teal-dim); border-radius:7px; padding:4px 10px;}
.topictag{font-family:var(--code); font-size:10.5px; font-weight:700; color:var(--amber); letter-spacing:.5px;}
.task h3{font-size:16.5px; margin:6px 0 8px;}
.task .prompt{color:var(--text-1); font-size:13.5px; margin-bottom:14px;}
.task .prompt code{color:var(--purple);}

.codebox{font-family:var(--code); font-size:12px; white-space:pre-wrap; word-break:break-word; background:var(--bg-0); border:1px solid var(--border); border-radius:9px; padding:12px 14px; margin-bottom:12px; color:var(--text-0);}

/* reorder tiles */
.tilerow{display:flex; gap:8px; flex-wrap:wrap; margin-bottom:10px;}
.tile{background:var(--bg-2); border:1px solid var(--border-strong); border-radius:9px; padding:10px 12px; display:flex; align-items:center; gap:8px; font-size:12.5px; font-weight:600;}
.tile button{width:22px; height:22px; border-radius:5px; background:var(--bg-3); font-size:11px; border:1px solid var(--border);}
.tile button:disabled{opacity:.3;}

/* scenario mcq */
.scenario{border:1px solid var(--border); border-radius:9px; padding:10px 12px; margin-bottom:8px; background:var(--bg-0);}
.scenario .snip{font-family:var(--code); font-size:12px; margin-bottom:8px; color:var(--text-0);}
.scenario select{background:var(--bg-2); border:1px solid var(--border-strong); border-radius:6px; padding:6px 8px; font-size:12px; width:100%;}

/* classify */
.classrow{display:flex; justify-content:space-between; align-items:center; gap:10px; border:1px solid var(--border); border-radius:9px; padding:10px 12px; margin-bottom:8px; background:var(--bg-0);}
.classrow .txt{font-size:12.5px; flex:1;}
.classbtn{font-size:11px; font-weight:700; padding:6px 12px; border-radius:7px; border:1px solid var(--border-strong); background:var(--bg-2); color:var(--text-2); min-width:110px; text-align:center;}
.classbtn.portable{background:var(--teal-dim); border-color:var(--teal); color:var(--teal);}
.classbtn.target{background:var(--amber-dim); border-color:var(--amber); color:var(--amber);}

/* inputs */
.textin{width:100%; background:var(--bg-2); border:1px solid var(--border-strong); border-radius:8px; padding:9px 12px; font-size:13px;}
textarea.textin{min-height:90px; resize:vertical;}
.numin{width:220px;}
.fieldlabel{font-size:11.5px; color:var(--text-2); margin:8px 0 5px; font-family:var(--code);}

/* fill blanks */
.blankcode{font-family:var(--code); font-size:12px; white-space:pre-wrap; background:var(--bg-0); border:1px solid var(--border); border-radius:9px; padding:12px 14px; line-height:2;}
.blankin{background:var(--bg-3); border:1px solid var(--amber); border-radius:5px; padding:1px 6px; font-size:12px; width:120px; color:var(--amber); font-weight:700;}

/* reveal panel */
.revealwrap{margin-top:14px; border-radius:10px; overflow:hidden; border:1px solid var(--border-strong);}
.revealhead{background:var(--bg-2); padding:9px 14px; font-family:var(--code); font-size:11px; font-weight:800; color:var(--text-2); display:flex; align-items:center; gap:8px;}
.revealbody{padding:14px; background:var(--bg-0); font-size:13px; color:var(--text-1); display:none;}
.revealbody.show{display:block;}
.locked .revealbody{display:none;}
.locked .revealhead{color:var(--text-2);}
.revealbody .codebox{margin:8px 0 0; background:var(--bg-1);}
.gradepill{font-size:10.5px; font-weight:800; padding:3px 9px; border-radius:20px; margin-left:auto;}
.gradepill.correct{background:var(--green-dim); color:var(--green);}
.gradepill.wrong{background:var(--red-dim); color:var(--red);}

/* trainer unlock */
.trainerbox{max-width:980px; margin:0 auto 60px; background:var(--bg-1); border:2px solid var(--amber); border-radius:14px; padding:22px 24px;}
.trainerbox h3{color:var(--amber); margin-bottom:8px; font-size:16px;}
.trainerbox p{color:var(--text-1); font-size:13px; margin-bottom:14px;}
.trainerrow{display:flex; gap:10px; flex-wrap:wrap; align-items:center;}
.trainerrow input{background:var(--bg-2); border:1px solid var(--border-strong); border-radius:8px; padding:9px 12px; font-size:13px; min-width:220px;}
.btn{border-radius:9px; padding:10px 18px; font-size:13px; font-weight:700; transition:.15s;}
.btn.primary{background:var(--teal); color:#04231d;}
.btn.primary:hover{filter:brightness(1.1);}
.btn.amber{background:var(--amber); color:#2b1c02;}
.unlockmsg{font-family:var(--code); font-size:12px; margin-left:8px;}
.unlockmsg.ok{color:var(--green);}
.unlockmsg.bad{color:var(--red);}

.footer-note{text-align:center; color:var(--text-2); font-size:11px; padding:10px 0 30px; font-family:var(--code);}
</style>
</head>
<body>

<header>
  <div class="eyebrow">2-HOUR LAB EXERCISE</div>
  <h1>Build Process, Toolchain, Porting, Linker Script &amp; startup.S</h1>
  <p>12 tasks across everything covered in the lecture. Work through them in any order — your answers save automatically in this browser. Answers are hidden until your trainer unlocks them at the end.</p>
  <div class="timebox">⏱ Budget: ~10 minutes per task, 2 hours total</div>
</header>

<div class="namebar">
  <div><label>Name</label><input type="text" id="studentName" placeholder="Your name"></div>
  <div><label>Roll #</label><input type="text" id="studentRoll" placeholder="Roll number"></div>
  <div class="saved" id="savedIndicator"></div>
</div>

<nav class="jumpnav" id="jumpNav"></nav>

<main id="taskContainer"></main>

<div class="trainerbox">
  <h3>🔒 Trainer Answer Key</h3>
  <p>Once unlocked, every task's correct/model answer becomes visible below its own answer box, for the whole session — including any auto-checkable tasks showing whether the student's saved answer was correct.</p>
  <div class="trainerrow">
    <input type="password" id="trainerPw" placeholder="Trainer password">
    <button class="btn amber" onclick="unlockAnswers()">Unlock Answer Key</button>
    <span class="unlockmsg" id="unlockMsg"></span>
  </div>
</div>

<div class="footer-note">Answers save locally in this browser only — this is a classroom convenience, not real security.</div>

<script>
function esc(s){ return String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;'); }
const TRAINER_PASSWORD = 'abcd@4321';
let unlocked = false;

/* ============================================================
   STORAGE
============================================================ */
const STORE_KEY = 'lab2hr_answers_v1';
function loadStore(){
  try { return JSON.parse(localStorage.getItem(STORE_KEY) || '{}'); } catch(e){ return {}; }
}
function saveStore(store){
  try { localStorage.setItem(STORE_KEY, JSON.stringify(store)); } catch(e){}
  const ind = document.getElementById('savedIndicator');
  ind.textContent = 'saved ' + new Date().toLocaleTimeString();
}
const STORE = loadStore();

/* ============================================================
   TASK DEFINITIONS
============================================================ */
const TASKS = [
  { id:'t1', topic:'BUILD PROCESS', title:'Order the Build Pipeline', type:'reorder',
    prompt:'Arrange these four stages into the correct build order.',
    items:['Linker','Source Code','Assembler','Compiler'],
    correct:['Source Code','Compiler','Assembler','Linker'] },

  { id:'t2', topic:'BUILD PROCESS', title:'Which Stage Catches This Bug?', type:'scenario-mcq',
    prompt:'For each broken snippet, select the build stage that would actually catch the problem.',
    options:['Preprocessor','Compiler','Assembler','Linker'],
    parts:[
      { snip:'#include "config_missing.h"   // this file was deleted', correct:'Preprocessor' },
      { snip:'int x = 5   // missing semicolon', correct:'Compiler' },
      { snip:'void init() defined in BOTH main.c and driver.c', correct:'Linker' },
      { snip:'asm("frobnicate r0")   // not a real instruction', correct:'Assembler' },
    ] },

  { id:'t3', topic:'BUILD PROCESS', title:'Read a Real Object Dump', type:'numeric-parts',
    prompt:'Study this real disassembly, then answer both questions below it.',
    code:`08000158 <digitalWrite>:
 8000158: b508      push {r3, lr}
 800015a: 4b06      ldr  r3, [pc, #24]
 800015c: 681a      ldr  r2, [r3, #0]
 800015e: 2900      cmp  r1, #0
 8000160: d003      beq.n 800016a
 8000162: 2401      movs r4, #1
 8000164: 4084      lsls r4, r0
 8000166: 4323      orrs r3, r4
 8000168: e001      b.n  800016e
 800016a: 2401      movs r4, #1
 800016c: 4084      lsls r4, r0
 800016e: 601a      str  r2, [r3, #0]
 8000170: bd08      pop  {r3, pc}`,
    parts:[
      { label:'Address of digitalWrite\u2019s very first instruction:', correct:'0x08000158' },
      { label:'Total size of this function, in bytes (last instruction is 2 bytes):', correct:'26' },
    ] },

  { id:'t4', topic:'TOOLCHAIN', title:'Why a Cross-Compiler?', type:'shortanswer',
    prompt:'In 2\u20133 sentences: why does embedded development require a cross-compiler, and what would go wrong with a native (host) compiler instead?',
    modelAnswer:'A cross-compiler runs on your PC (the host) but produces machine code for a completely different CPU (the target, e.g. ARM or RISC-V) \u2014 the target chip has no OS and nowhere near enough resources to compile its own code. A native compiler produces code for the SAME architecture it runs on, so using one for embedded development would generate x86 instructions that the target microcontroller physically cannot execute.' },

  { id:'t5', topic:'TOOLCHAIN', title:'OpenOCD\u2019s Two Jobs', type:'shortanswer',
    prompt:'Describe, step by step, what OpenOCD actually does during the Flash step, and separately during the Debug step.',
    modelAnswer:'Flash step: OpenOCD halts the CPU, erases the relevant flash sectors, writes the new firmware bytes, reads them back to verify, then releases reset so the chip boots the new program. Debug step: OpenOCD keeps the SWD/JTAG connection open and, on request from the IDE/GDB, halts the running CPU, reads out register and memory values, and reports them back \u2014 enabling breakpoints and live inspection.' },

  { id:'t6', topic:'PORTING', title:'Calculate the Ported Address', type:'fillnumeric',
    prompt:'STRIVE-I places every peripheral\u2019s registers starting at base address 0x80000000, with each peripheral\u2019s block exactly 0x1000 bytes apart. GPIO is peripheral #0. Your assigned peripheral, Timer, is peripheral #4. What is Timer\u2019s base address?',
    correct:'0x80004000' },

  { id:'t7', topic:'PORTING', title:'Portable or Target-Specific?', type:'classify',
    prompt:'Click each item to cycle: unset \u2192 Portable \u2192 Target-Specific.',
    items:[
      { text:'Application logic in main.c', correct:'portable' },
      { text:'Register addresses in the driver .c file', correct:'target' },
      { text:'Function prototypes in the driver .h file', correct:'portable' },
      { text:'Clock configuration values', correct:'target' },
      { text:'The linker script', correct:'target' },
      { text:'The public API function names', correct:'portable' },
    ] },

  { id:'t8', topic:'LINKER SCRIPT', title:'Write a MEMORY Block', type:'codewrite',
    prompt:'Your assigned chip: FLASH starts at 0x08000000, 256K in size. RAM starts at 0x20000000, 64K in size. Write the complete MEMORY block.',
    modelAnswer:`MEMORY
{
  FLASH (rx)  : ORIGIN = 0x08000000, LENGTH = 256K
  RAM   (rwx) : ORIGIN = 0x20000000, LENGTH = 64K
}` },

  { id:'t9', topic:'LINKER SCRIPT', title:'Complete the SECTIONS Block', type:'fillblanks',
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

  { id:'t10', topic:'LINKER SCRIPT', title:'Why Two Placement Rules?', type:'shortanswer',
    prompt:'Explain why .data\u2019s placement rule needs both "> RAM" and "AT > FLASH". What would break if you only wrote "> RAM"?',
    modelAnswer:'"> RAM" tells the linker where the variable lives while the program runs (its working, writable address). "AT > FLASH" tells it to also keep a permanent stored copy of the initial value in FLASH, since FLASH survives power-off and RAM doesn\u2019t. With only "> RAM", there would be no permanent copy anywhere, and startup.S would have nothing valid to copy from \u2014 every initialised global would start as garbage instead of its intended value.' },

  { id:'t11', topic:'STARTUP.S', title:'Order the Boot Sequence', type:'reorder',
    prompt:'Arrange these six events into the order they actually happen after power-on.',
    items:['Call main()','Set the stack pointer','Power-on reset, PC jumps to _start','Loop forever if main() returns','Copy .data from FLASH to RAM','Clear .bss to zero'],
    correct:['Power-on reset, PC jumps to _start','Set the stack pointer','Copy .data from FLASH to RAM','Clear .bss to zero','Call main()','Loop forever if main() returns'] },

  { id:'t12', topic:'STARTUP.S', title:'Complete the .bss Clearing Loop', type:'fillblanks',
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
];

/* ============================================================
   GENERIC HELPERS
============================================================ */
function getAnswer(taskId, key){
  return (STORE[taskId] && STORE[taskId][key] !== undefined) ? STORE[taskId][key] : undefined;
}
function setAnswer(taskId, key, value){
  if(!STORE[taskId]) STORE[taskId] = {};
  STORE[taskId][key] = value;
  saveStore(STORE);
  updateJumpNav();
}
function taskHasAnyAnswer(taskId){
  const t = STORE[taskId];
  if(!t) return false;
  return Object.values(t).some(v => v !== undefined && v !== null && String(v).trim() !== '');
}

/* ============================================================
   RENDERERS PER TASK TYPE
============================================================ */
function renderReorder(task, body){
  let order = getAnswer(task.id, 'order');
  if(!order) order = task.items.slice();
  setAnswer(task.id, 'order', order);

  const row = document.createElement('div');
  row.className = 'tilerow';
  body.appendChild(row);

  function draw(){
    row.innerHTML = '';
    order.forEach((label, i)=>{
      const tile = document.createElement('div');
      tile.className = 'tile';
      tile.innerHTML = `<button ${i===0?'disabled':''} data-dir="-1">\u25C0</button><span>${esc(label)}</span><button ${i===order.length-1?'disabled':''} data-dir="1">\u25B6</button>`;
      const [leftBtn, , rightBtn] = tile.children;
      leftBtn.onclick = () => { [order[i-1],order[i]]=[order[i],order[i-1]]; setAnswer(task.id,'order',order); draw(); };
      rightBtn.onclick = () => { [order[i+1],order[i]]=[order[i],order[i+1]]; setAnswer(task.id,'order',order); draw(); };
      row.appendChild(tile);
    });
  }
  draw();

  return () => {
    const currentOrder = getAnswer(task.id, 'order') || order;
    const ok = JSON.stringify(currentOrder) === JSON.stringify(task.correct);
    return `<div>Correct order:</div><div class="codebox">${task.correct.map((x,i)=>(i+1)+'. '+esc(x)).join('\n')}</div>`
      + gradePill(taskHasAnyAnswer(task.id) ? ok : null);
  };
}

function renderScenarioMcq(task, body){
  task.parts.forEach((p, i)=>{
    const key = 'p' + i;
    const div = document.createElement('div');
    div.className = 'scenario';
    const saved = getAnswer(task.id, key) || '';
    div.innerHTML = `<div class="snip">${esc(p.snip)}</div>
      <select>
        <option value="">\u2014 choose a stage \u2014</option>
        ${task.options.map(o=>`<option value="${esc(o)}" ${o===saved?'selected':''}>${esc(o)}</option>`).join('')}
      </select>`;
    div.querySelector('select').onchange = (e) => setAnswer(task.id, key, e.target.value);
    body.appendChild(div);
  });

  return () => {
    let rows = task.parts.map((p,i)=>{
      const given = getAnswer(task.id,'p'+i);
      const ok = given === p.correct;
      return `<div style="margin-bottom:6px;">${esc(p.snip)} \u2192 <b style="color:var(--green);">${esc(p.correct)}</b> ${given!==undefined ? gradePill(ok) : ''}</div>`;
    }).join('');
    return rows;
  };
}

function renderNumericParts(task, body){
  if(task.code){
    const cb = document.createElement('div');
    cb.className = 'codebox';
    cb.textContent = task.code;
    body.appendChild(cb);
  }
  task.parts.forEach((p,i)=>{
    const key = 'p'+i;
    const lbl = document.createElement('div');
    lbl.className = 'fieldlabel';
    lbl.textContent = p.label;
    body.appendChild(lbl);
    const inp = document.createElement('input');
    inp.className = 'textin numin';
    inp.value = getAnswer(task.id, key) || '';
    inp.oninput = () => setAnswer(task.id, key, inp.value);
    body.appendChild(inp);
  });

  return () => task.parts.map((p,i)=>{
    const given = (getAnswer(task.id,'p'+i) || '').trim();
    const ok = given.toLowerCase() === p.correct.toLowerCase();
    return `<div style="margin-bottom:6px;">${esc(p.label)} <b style="color:var(--green);">${esc(p.correct)}</b> ${given ? gradePill(ok) : ''}</div>`;
  }).join('');
}

function renderShortAnswer(task, body){
  const ta = document.createElement('textarea');
  ta.className = 'textin';
  ta.placeholder = 'Type your answer here...';
  ta.value = getAnswer(task.id, 'text') || '';
  ta.oninput = () => setAnswer(task.id, 'text', ta.value);
  body.appendChild(ta);

  return () => `<div class="fieldlabel" style="margin-top:0;">MODEL ANSWER (for comparison, not the only acceptable wording)</div><div class="codebox" style="white-space:pre-wrap; font-family:var(--ui);">${esc(task.modelAnswer)}</div>`;
}

function renderFillNumeric(task, body){
  const inp = document.createElement('input');
  inp.className = 'textin numin';
  inp.value = getAnswer(task.id, 'val') || '';
  inp.oninput = () => setAnswer(task.id, 'val', inp.value);
  body.appendChild(inp);

  return () => {
    const given = (getAnswer(task.id,'val')||'').trim().toLowerCase();
    const ok = given === task.correct.toLowerCase();
    return `Correct answer: <b style="color:var(--green);">${esc(task.correct)}</b> ${given ? gradePill(ok) : ''}`;
  };
}

function renderClassify(task, body){
  task.items.forEach((it, i)=>{
    const key = 'c'+i;
    const row = document.createElement('div');
    row.className = 'classrow';
    let state = getAnswer(task.id, key) || '';
    const label = (s) => s==='portable' ? 'Portable' : s==='target' ? 'Target-Specific' : 'Click to classify';
    row.innerHTML = `<span class="txt">${esc(it.text)}</span><button class="classbtn ${state}">${label(state)}</button>`;
    const btn = row.querySelector('button');
    btn.onclick = () => {
      state = state === '' ? 'portable' : state === 'portable' ? 'target' : '';
      setAnswer(task.id, key, state);
      btn.className = 'classbtn ' + state;
      btn.textContent = label(state);
    };
    body.appendChild(row);
  });

  return () => task.items.map((it,i)=>{
    const given = getAnswer(task.id,'c'+i);
    const ok = given === it.correct;
    return `<div style="margin-bottom:6px;">${esc(it.text)} \u2192 <b style="color:var(--green);">${it.correct==='portable'?'Portable':'Target-Specific'}</b> ${given ? gradePill(ok) : ''}</div>`;
  }).join('');
}

function renderCodeWrite(task, body){
  const ta = document.createElement('textarea');
  ta.className = 'textin';
  ta.style.minHeight = '130px';
  ta.placeholder = 'Write your code here...';
  ta.value = getAnswer(task.id, 'code') || '';
  ta.oninput = () => setAnswer(task.id, 'code', ta.value);
  body.appendChild(ta);

  return () => `<div class="fieldlabel" style="margin-top:0;">MODEL ANSWER</div><div class="codebox">${esc(task.modelAnswer)}</div>`;
}

function renderFillBlanks(task, body){
  const box = document.createElement('div');
  box.className = 'blankcode';
  body.appendChild(box);

  function draw(){
    box.innerHTML = '';
    const parts = task.template.split(/(\{\{B\d+\}\})/);
    parts.forEach(part=>{
      const m = part.match(/\{\{(B\d+)\}\}/);
      if(m){
        const bid = m[1];
        const inp = document.createElement('input');
        inp.className = 'blankin';
        inp.value = getAnswer(task.id, bid) || '';
        inp.oninput = () => setAnswer(task.id, bid, inp.value);
        box.appendChild(inp);
      } else if(part){
        box.appendChild(document.createTextNode(part));
      }
    });
  }
  draw();

  return () => {
    let out = '<div class="fieldlabel" style="margin-top:0;">CORRECT VALUES</div>';
    out += Object.keys(task.blanks).map(bid=>{
      const given = (getAnswer(task.id,bid)||'').trim();
      const ok = given === task.blanks[bid];
      return `<div style="margin-bottom:4px;">${bid}: <b style="color:var(--green);">${esc(task.blanks[bid])}</b> ${given ? gradePill(ok) : ''}</div>`;
    }).join('');
    return out;
  };
}

function gradePill(ok){
  if(ok === null || ok === undefined) return '';
  return `<span class="gradepill ${ok?'correct':'wrong'}">${ok?'\u2713 correct':'\u2717 check again'}</span>`;
}

/* ============================================================
   TASK CARD ASSEMBLY
============================================================ */
const RENDERERS = {
  'reorder': renderReorder,
  'scenario-mcq': renderScenarioMcq,
  'numeric-parts': renderNumericParts,
  'shortanswer': renderShortAnswer,
  'fillnumeric': renderFillNumeric,
  'classify': renderClassify,
  'codewrite': renderCodeWrite,
  'fillblanks': renderFillBlanks,
};
const revealFns = {};

function buildTaskCard(task, index){
  const card = document.createElement('div');
  card.className = 'task';
  card.id = 'task-' + task.id;
  card.innerHTML = `
    <div class="taskhead">
      <span class="tasknum">TASK ${index+1} / ${TASKS.length}</span>
      <span class="topictag">${esc(task.topic)}</span>
    </div>
    <h3>${esc(task.title)}</h3>
    <div class="prompt">${task.prompt}</div>
  `;
  const body = document.createElement('div');
  card.appendChild(body);

  const renderer = RENDERERS[task.type];
  const getReveal = renderer(task, body);
  revealFns[task.id] = getReveal;

  const revealWrap = document.createElement('div');
  revealWrap.className = 'revealwrap locked';
  revealWrap.id = 'reveal-' + task.id;
  revealWrap.innerHTML = `<div class="revealhead">🔒 ANSWER LOCKED — trainer unlock required</div><div class="revealbody"></div>`;
  card.appendChild(revealWrap);

  document.getElementById('taskContainer').appendChild(card);
}

function updateJumpNav(){
  document.querySelectorAll('.jumpbtn').forEach((btn,i)=>{
    btn.classList.toggle('answered', taskHasAnyAnswer(TASKS[i].id));
  });
}
function buildJumpNav(){
  const nav = document.getElementById('jumpNav');
  nav.innerHTML = '';
  TASKS.forEach((t,i)=>{
    const btn = document.createElement('button');
    btn.className = 'jumpbtn';
    btn.textContent = i+1;
    btn.title = t.title;
    btn.onclick = () => document.getElementById('task-'+t.id).scrollIntoView({behavior:'smooth', block:'start'});
    nav.appendChild(btn);
  });
  updateJumpNav();
}

/* ============================================================
   TRAINER UNLOCK
============================================================ */
function unlockAnswers(){
  const pw = document.getElementById('trainerPw').value;
  const msg = document.getElementById('unlockMsg');
  if(pw !== TRAINER_PASSWORD){
    msg.textContent = 'Incorrect password.';
    msg.className = 'unlockmsg bad';
    return;
  }
  unlocked = true;
  msg.textContent = 'Unlocked — scroll up to review every task.';
  msg.className = 'unlockmsg ok';
  TASKS.forEach(task=>{
    const wrap = document.getElementById('reveal-' + task.id);
    wrap.classList.remove('locked');
    wrap.querySelector('.revealhead').textContent = '🔓 ANSWER KEY';
    const bodyEl = wrap.querySelector('.revealbody');
    bodyEl.innerHTML = revealFns[task.id]();
    bodyEl.classList.add('show');
  });
}

/* ============================================================
   INIT
============================================================ */
document.getElementById('studentName').value = localStorage.getItem('lab2hr_name') || '';
document.getElementById('studentRoll').value = localStorage.getItem('lab2hr_roll') || '';
document.getElementById('studentName').oninput = (e) => localStorage.setItem('lab2hr_name', e.target.value);
document.getElementById('studentRoll').oninput = (e) => localStorage.setItem('lab2hr_roll', e.target.value);

TASKS.forEach((t,i)=>buildTaskCard(t,i));
buildJumpNav();
</script>
</body>
</html>
_2hour_exercise.html…]()


## END 

======================================================

## START

## Every C program becomes numbers in boxes




[Uploading <!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>RAM, FLASH & Your Program — A Guided Lesson</title>
<style>
:root{
  --bg-0:#0b0e14; --bg-1:#12161f; --bg-2:#181e2b; --bg-3:#212a3d;
  --border:#262f45; --border-strong:#38456334;
  --border-strong2:#3a4864;
  --text-0:#eef2f9; --text-1:#aab6ca; --text-2:#707d95;
  --teal:#33e0c4; --teal-dim:#0f342f;
  --amber:#ffb84d; --amber-dim:#3a2a10;
  --coral:#ff8a76; --coral-dim:#3a1a16;
  --green:#6ee7a8; --green-dim:#123527;
  --purple:#b491ff; --purple-dim:#241a3a;
  --code:'JetBrains Mono','Fira Code',ui-monospace,Consolas,monospace;
  --ui:-apple-system,'Segoe UI',Inter,sans-serif;
}
*{box-sizing:border-box; margin:0; padding:0;}
body{font-family:var(--ui); background:var(--bg-0); color:var(--text-0); min-height:100vh; display:flex; flex-direction:column;}
button{font-family:var(--ui); cursor:pointer; color:inherit; border:none; background:none;}
code{font-family:var(--code);}
h2{font-size:24px; margin-bottom:10px;}
h3{font-size:16px; margin-bottom:8px;}
p{line-height:1.6;}

/* ---------- Top progress trail ---------- */
.topbar{padding:16px 20px 0; max-width:880px; margin:0 auto; width:100%;}
.brand{font-family:var(--code); font-size:12px; color:var(--teal); font-weight:700; letter-spacing:1px; margin-bottom:12px;}
.trail{display:flex; gap:5px;}
.trail-seg{flex:1; height:6px; border-radius:4px; background:var(--bg-2); border:1px solid var(--border); cursor:pointer; transition:.15s;}
.trail-seg:hover{border-color:var(--border-strong2);}
.trail-seg.done{background:var(--teal); border-color:var(--teal);}
.trail-seg.current{background:var(--amber); border-color:var(--amber);}
.trail-caption{font-family:var(--code); font-size:11px; color:var(--text-2); margin-top:8px;}

/* ---------- Main card viewport ---------- */
main{flex:1; display:flex; align-items:center; justify-content:center; padding:24px 20px;}
.card{
  max-width:840px; width:100%; background:var(--bg-1); border:1px solid var(--border); border-radius:18px;
  padding:36px 40px; animation:cardIn .35s ease;
}
@keyframes cardIn{ from{opacity:0; transform:translateY(10px);} to{opacity:1; transform:translateY(0);} }
.eyebrow{font-family:var(--code); font-size:11.5px; color:var(--teal); letter-spacing:1.5px; font-weight:700; margin-bottom:10px;}
.analogy{
  background:var(--bg-2); border-left:3px solid var(--purple); border-radius:0 10px 10px 0; padding:14px 18px; margin:16px 0;
  font-size:14.5px; color:var(--text-1); font-style:italic;
}
.analogy b{color:var(--purple); font-style:normal;}
.lede{color:var(--text-1); font-size:14.5px; margin-bottom:6px;}

.codebox{
  font-family:var(--code); font-size:12.5px; line-height:1.75; background:var(--bg-0); border:1px solid var(--border);
  border-radius:10px; padding:14px 16px; white-space:pre-wrap; word-break:break-word; color:var(--text-0); margin:14px 0;
}
.codebox .hl{color:var(--amber); font-weight:700;}
.codebox .hl2{color:var(--teal); font-weight:700;}
.codebox .cm{color:var(--text-2); font-style:italic;}

.widget{ background:var(--bg-0); border:1px solid var(--border); border-radius:12px; padding:22px; margin:16px 0; min-height:120px; }
.widget-row{display:flex; gap:12px; align-items:center; flex-wrap:wrap; justify-content:center;}
.btn{border-radius:9px; padding:10px 18px; font-size:13px; font-weight:700; transition:.15s; border:1px solid transparent;}
.btn.primary{background:var(--teal); color:#04231d;}
.btn.primary:hover{filter:brightness(1.1);}
.btn.secondary{background:var(--bg-2); color:var(--text-0); border-color:var(--border-strong2);}
.btn.secondary:hover{border-color:var(--teal); color:var(--teal);}
.btn:disabled{opacity:.35; cursor:not-allowed;}

/* lockers (RAM) */
.lockerrow{display:flex; gap:8px; justify-content:center;}
.locker{width:56px; height:56px; border-radius:8px; background:var(--bg-2); border:1px solid var(--border-strong2); display:flex; align-items:center; justify-content:center; font-family:var(--code); font-size:11px; color:var(--text-2); position:relative; transition:.3s;}
.locker.lit{background:var(--teal-dim); border-color:var(--teal); color:var(--teal); font-weight:800;}
.locker .addr{position:absolute; bottom:-18px; font-size:9px; color:var(--text-2);}
.locker .lbl{position:absolute; top:-24px; font-size:10px; color:var(--teal); font-weight:700; opacity:0; transition:opacity .3s;}
.locker.lit .lbl{opacity:1;}

/* FLASH vs RAM power demo */
.pairbox{display:flex; gap:30px; justify-content:center; align-items:flex-start;}
.chipbox{width:150px; border-radius:10px; border:1.5px solid var(--border-strong2); background:var(--bg-2); padding:14px; text-align:center;}
.chipbox h4{font-family:var(--code); font-size:12.5px; margin-bottom:10px;}
.chipbox .val{font-family:var(--code); font-size:18px; font-weight:800; padding:10px; border-radius:8px; background:var(--bg-1); transition:.4s;}
.chipbox.flash h4{color:#7cc7ff;}
.chipbox.ram h4{color:var(--amber);}
.chipbox .val.forgot{color:var(--text-2);}
.chipbox .val.remembers{color:var(--green);}

/* data copy demo */
.copyrow{display:flex; align-items:center; justify-content:center; gap:16px;}
.copybox{width:180px; height:70px; border-radius:10px; border:1.5px solid var(--border-strong2); background:var(--bg-2); display:flex; flex-direction:column; align-items:center; justify-content:center; font-family:var(--code); font-size:12px; position:relative;}
.copybox.flashc{border-color:#7cc7ff;}
.copybox.ramc{border-color:var(--amber);}
.copybox .tag{font-size:10px; color:var(--text-2); margin-bottom:4px;}
.copybox .num{font-size:16px; font-weight:800;}
.copyarrow{width:70px; height:26px; position:relative;}
.dot{position:absolute; width:12px; height:12px; border-radius:50%; background:var(--amber); top:7px; left:0; opacity:0; box-shadow:0 0 8px 2px rgba(255,184,77,.6);}
.dot.flying{animation:flyDot 1s ease forwards;}
@keyframes flyDot{ 0%{opacity:0; left:0;} 15%{opacity:1;} 85%{opacity:1;} 100%{opacity:0; left:58px;} }
.ramc.filled .num{color:var(--green);}

/* bss demo */
.bsscell{width:200px; height:70px; border-radius:10px; border:1.5px dashed var(--border-strong2); background:var(--bg-2); display:flex; flex-direction:column; align-items:center; justify-content:center; font-family:var(--code); margin:0 auto; transition:.4s;}
.bsscell.cleared{border-style:solid; border-color:var(--green); background:var(--green-dim);}
.bsscell .num{font-size:16px; font-weight:800; color:var(--text-2);}
.bsscell.cleared .num{color:var(--green);}

/* stack plates */
.stackwidget{display:flex; flex-direction:column-reverse; align-items:center; gap:6px; min-height:210px; justify-content:flex-start;}
.plate{width:170px; height:34px; border-radius:8px; background:linear-gradient(180deg,#dcc8ff,#b491ff); color:#241a3a; font-family:var(--code); font-weight:800; font-size:12px; display:flex; align-items:center; justify-content:center; animation:plateIn .3s ease;}
@keyframes plateIn{ from{opacity:0; transform:translateY(-14px) scale(.9);} to{opacity:1; transform:translateY(0) scale(1);} }
.plate.leaving{animation:plateOut .25s ease forwards;}
@keyframes plateOut{ to{opacity:0; transform:translateY(-14px) scale(.9);} }
.spline{font-family:var(--code); font-size:11px; color:var(--purple); margin-top:6px;}

/* predict-reveal */
.predict{margin:16px 0;}
.predict .q{font-size:13.5px; font-weight:700; margin-bottom:10px; color:var(--text-0);}
.reveal-box{
  margin-top:12px; background:var(--bg-2); border:1px solid var(--border-strong2); border-radius:10px; padding:14px 16px;
  font-size:13.5px; color:var(--text-1); display:none;
}
.reveal-box.show{display:block; animation:cardIn .3s ease;}

/* quiz */
.qopt{display:block; width:100%; text-align:left; background:var(--bg-2); border:1px solid var(--border-strong2); border-radius:9px; padding:11px 14px; font-size:13.5px; color:var(--text-1); margin-bottom:8px; transition:.15s;}
.qopt:hover:not(:disabled){border-color:var(--teal);}
.qopt.correct{border-color:var(--green); background:var(--green-dim); color:var(--green);}
.qopt.wrong{border-color:var(--coral); background:var(--coral-dim); color:var(--coral);}
.qopt:disabled{cursor:default;}

/* recap checklist */
.checkrow{display:flex; gap:10px; align-items:flex-start; margin-bottom:10px; font-size:13.5px; color:var(--text-1);}
.checkrow .tick{color:var(--green); font-weight:800; flex-shrink:0;}

/* glossary terms */
.gloss{border:1px solid var(--border); border-radius:10px; padding:13px 16px; margin-bottom:10px; background:var(--bg-0);}
.gloss .term{font-family:var(--code); font-weight:800; font-size:13px; color:var(--teal); margin-bottom:5px;}
.gloss .term .ex{font-weight:500; color:var(--text-2); font-size:11.5px; margin-left:8px;}
.gloss .def{font-size:13px; color:var(--text-1);}
.gloss-group-label{font-family:var(--code); font-size:11px; font-weight:800; color:var(--amber); letter-spacing:1px; margin:16px 0 8px;}
.gloss-group-label:first-child{margin-top:0;}
.scroll-note{font-size:11.5px; color:var(--text-2); text-align:center; margin-top:10px; font-style:italic;}

/* nav */
.navbar{max-width:840px; margin:0 auto; width:100%; padding:0 20px 26px; display:flex; justify-content:space-between; gap:10px;}
.footer-note{text-align:center; color:var(--text-2); font-size:11px; padding:6px 0 20px; font-family:var(--code);}
@media (max-width:640px){ .card{padding:26px 22px;} .pairbox{flex-direction:column; align-items:center;} }
</style>
</head>
<body>

<div class="topbar">
  <div class="brand">RAM, FLASH &amp; YOUR PROGRAM — GUIDED LESSON</div>
  <div class="trail" id="trail"></div>
  <div class="trail-caption" id="trailCaption"></div>
</div>

<main><div class="card" id="cardRoot"></div></main>

<div class="navbar">
  <button class="btn secondary" id="backBtn" onclick="go(-1)">◀ Back</button>
  <button class="btn primary" id="nextBtn" onclick="go(1)">Next ▶</button>
</div>
<div class="footer-note">Click-paced &middot; nothing moves until you tell it to</div>

<script>
function esc(s){ return String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;'); }

/* ============================================================
   CARD 0 — Welcome + the code
============================================================ */
function buildIntro(root){
  root.innerHTML = `
    <div class="eyebrow">BEFORE WE START</div>
    <h2>Every C program becomes numbers in boxes</h2>
    <p class="lede">That's really it. This whole lesson is about answering one question, piece by piece: <b>for each part of your code, which box does it end up in, and who put it there?</b></p>
    <div class="analogy">We'll use one tiny, fixed piece of code for the entire lesson — so by the end, you'll be able to point at any line of it and say exactly where it lives.</div>
    <div class="codebox">int counter = 5;        <span class="cm">// a number that starts at 5</span>
int total;               <span class="cm">// a number with no starting value</span>
const int MAX = 100;     <span class="cm">// a number that never changes</span>

int add(int a, int b)   <span class="cm">// a small function</span>
{
    int result = a + b; <span class="cm">// exists only briefly</span>
    return result;
}</div>
    <p class="lede">Five things. Five different answers to "which box, and who put it there." Click Next when you're ready.</p>
  `;
}

/* ============================================================
   CARD 1 — What is RAM?
============================================================ */
function buildRam(root){
  root.innerHTML = `
    <div class="eyebrow">CONCEPT 1 OF 11</div>
    <h2>What is RAM, really?</h2>
    <div class="analogy">Picture a wall of small numbered lockers. <b>RAM is just that</b> — thousands of tiny numbered storage boxes, sitting inside the chip.</div>
    <p class="lede">Each locker's number is called its <b>address</b>. Click a locker below.</p>
    <div class="widget"><div class="lockerrow" id="lockerRow"></div></div>
    <p class="lede" style="margin-top:26px;">Whatever number you clicked — that's an address. A variable "living at an address" just means: its value sits inside that one specific locker.</p>
  `;
  const row = root.querySelector('#lockerRow');
  const addrs = ['0x00','0x04','0x08','0x0C','0x10','0x14'];
  addrs.forEach((a,i)=>{
    const el = document.createElement('div');
    el.className = 'locker';
    el.innerHTML = `<span class="lbl">here!</span>?<span class="addr">${a}</span>`;
    el.onclick = () => {
      row.querySelectorAll('.locker').forEach(x=>x.classList.remove('lit'));
      el.classList.add('lit');
      el.textContent = '';
      el.innerHTML = `<span class="lbl">here!</span>?<span class="addr">${a}</span>`;
    };
    row.appendChild(el);
  });
}

/* ============================================================
   CARD 2 — FLASH vs RAM (power toggle demo)
============================================================ */
function buildFlash(root){
  root.innerHTML = `
    <div class="eyebrow">CONCEPT 2 OF 11</div>
    <h2>FLASH remembers. RAM forgets.</h2>
    <div class="analogy">RAM is a whiteboard — fast to write on, but wiped clean the moment power is cut. <b>FLASH is a printed page</b> — slower to produce, but it survives power-off.</div>
    <div class="widget">
      <div class="pairbox">
        <div class="chipbox flash"><h4>FLASH</h4><div class="val remembers" id="flashVal">5</div></div>
        <div class="chipbox ram"><h4>RAM</h4><div class="val remembers" id="ramVal">5</div></div>
      </div>
      <div class="widget-row" style="margin-top:18px;">
        <button class="btn primary" id="powerBtn">⚡ Cut the power, then restore it</button>
      </div>
    </div>
    <p class="lede" id="flashExplain">Both start out holding the same value. Click the button and watch what survives.</p>
  `;
  const flashVal = root.querySelector('#flashVal');
  const ramVal = root.querySelector('#ramVal');
  const btn = root.querySelector('#powerBtn');
  const explain = root.querySelector('#flashExplain');
  btn.onclick = () => {
    ramVal.textContent = '?';
    ramVal.className = 'val forgot';
    explain.textContent = 'RAM lost its value the instant power was cut — that\'s just how RAM works. FLASH never even noticed the power blip.';
    btn.disabled = true;
  };
}

/* ============================================================
   CARD 3 — .text and .rodata (the easy cases)
============================================================ */
function buildTextRodata(root){
  root.innerHTML = `
    <div class="eyebrow">CONCEPT 3 OF 11</div>
    <h2>The two easy cases: code and constants</h2>
    <div class="analogy">Your compiled function and a value like <code>const int MAX = 100;</code> both have one thing in common: <b>they never change while the program runs.</b> So there's no reason they'd ever need to live in forgetful RAM.</div>
    <div class="codebox">const int MAX = 100;     <span class="hl">→ .rodata → FLASH</span>
int add(int a, int b) { .. }  <span class="hl">→ .text → FLASH</span></div>
    <p class="lede">Both get placed in FLASH once, when the chip is programmed, and never move again. This is the simplest possible case — nothing has to happen at start-up for either of these.</p>
  `;
}

/* ============================================================
   CARD 4 — .data (the hard one)
============================================================ */
function buildData(root){
  root.innerHTML = `
    <div class="eyebrow">CONCEPT 4 OF 11</div>
    <h2>counter = 5 — the one that needs TWO homes</h2>
    <div class="analogy">counter starts at 5, and that starting value must survive power-off — so far, that sounds like FLASH's job. But counter is a variable — your program is going to change it — and FLASH can't be written to while running. So it needs a home in RAM too.</div>
    <div class="predict">
      <div class="q">Before you click anything: where do you think the number 5 is stored FIRST — before your program even starts running?</div>
      <button class="btn secondary" onclick="this.nextElementSibling.classList.add('show'); this.disabled=true;">Reveal the answer</button>
      <div class="reveal-box">In FLASH. It has to be — RAM doesn't have anything in it yet at all when the chip first powers on.</div>
    </div>
    <div class="widget">
      <div class="copyrow">
        <div class="copybox flashc"><span class="tag">FLASH (stored copy)</span><span class="num">counter = 5</span></div>
        <div class="copyarrow"><div class="dot" id="dataDot"></div></div>
        <div class="copybox ramc" id="ramDataBox"><span class="tag">RAM (working copy)</span><span class="num">?</span></div>
      </div>
      <div class="widget-row" style="margin-top:18px;">
        <button class="btn primary" id="copyBtn">▶ Run the copy step</button>
      </div>
    </div>
    <p class="lede" id="dataExplain">This copy step is real code — a startup.S loop, which you'll see later — moving the 5 from FLASH into RAM.</p>
  `;
  const dot = root.querySelector('#dataDot');
  const ramBox = root.querySelector('#ramDataBox');
  const btn = root.querySelector('#copyBtn');
  btn.onclick = () => {
    dot.classList.remove('flying'); void dot.offsetWidth; dot.classList.add('flying');
    setTimeout(()=>{
      ramBox.classList.add('filled');
      ramBox.querySelector('.num').textContent = 'counter = 5';
    }, 850);
    btn.disabled = true;
  };
}

/* ============================================================
   CARD 5 — .bss
============================================================ */
function buildBss(root){
  root.innerHTML = `
    <div class="eyebrow">CONCEPT 5 OF 11</div>
    <h2>total — reserved, but never stored</h2>
    <div class="analogy">total has no starting value at all. There's nothing to copy from FLASH — so FLASH doesn't store anything for it, not even a zero.</div>
    <div class="predict">
      <div class="q">Before you click: right after power-on, before anything clears it, what do you think total's RAM slot actually contains?</div>
      <button class="btn secondary" onclick="this.nextElementSibling.classList.add('show'); this.disabled=true;">Reveal the answer</button>
      <div class="reveal-box">Garbage — whatever random electrical noise was sitting in that RAM cell before power-on. It is NOT automatically zero. Something has to actively make it zero.</div>
    </div>
    <div class="widget">
      <div class="bsscell" id="bssCell"><span class="tag" style="color:var(--text-2); font-size:10px;">total</span><span class="num">?????</span></div>
      <div class="widget-row" style="margin-top:18px;">
        <button class="btn primary" id="clearBtn">▶ Run the zero-clearing step</button>
      </div>
    </div>
    <p class="lede">This is startup.S writing a real, literal 0 into that RAM cell — one instruction, doing actual work, so that total reliably starts at zero every single time.</p>
  `;
  const cell = root.querySelector('#bssCell');
  const btn = root.querySelector('#clearBtn');
  btn.onclick = () => {
    cell.classList.add('cleared');
    cell.querySelector('.num').textContent = '0';
    btn.disabled = true;
  };
}

/* ============================================================
   CARD 6 — What is the stack
============================================================ */
let plateCount = 0;
function buildStackConcept(root){
  plateCount = 0;
  root.innerHTML = `
    <div class="eyebrow">CONCEPT 6 OF 11</div>
    <h2>The stack: a pile of plates</h2>
    <div class="analogy">You always add a new plate to the <b>top</b>. You always remove the <b>top</b> plate first, never one from the middle. That rule is called <b>LIFO</b> — Last In, First Out — and RAM's stack works exactly the same way.</div>
    <div class="widget">
      <div class="stackwidget" id="plateStack"></div>
      <div class="spline" id="spLine">SP → empty, nothing pushed yet</div>
      <div class="widget-row" style="margin-top:14px;">
        <button class="btn primary" id="pushBtn">Push a plate</button>
        <button class="btn secondary" id="popBtn">Pop the top plate</button>
      </div>
    </div>
    <p class="lede">Try it a few times — push 3 or 4 plates, then pop them. Notice you can only ever touch the top one.</p>
  `;
  const stackEl = root.querySelector('#plateStack');
  const spLine = root.querySelector('#spLine');
  const pushBtn = root.querySelector('#pushBtn');
  const popBtn = root.querySelector('#popBtn');
  pushBtn.onclick = () => {
    plateCount++;
    const p = document.createElement('div');
    p.className = 'plate';
    p.textContent = 'Plate ' + plateCount;
    stackEl.appendChild(p);
    spLine.textContent = `SP → points at plate ${plateCount} (the top)`;
  };
  popBtn.onclick = () => {
    const plates = stackEl.querySelectorAll('.plate');
    if(plates.length === 0) return;
    const top = plates[plates.length-1];
    top.classList.add('leaving');
    setTimeout(()=>top.remove(), 240);
    plateCount--;
    spLine.textContent = plateCount > 0 ? `SP → points at plate ${plateCount} (the top)` : 'SP → empty again';
  };
}

/* ============================================================
   CARD 7 — result on the stack
============================================================ */
function buildStackLocal(root){
  root.innerHTML = `
    <div class="eyebrow">CONCEPT 7 OF 11</div>
    <h2>result — born and gone, all on the stack</h2>
    <div class="codebox">int add(int a, int b)
{
    <span class="hl2">int result = a + b;</span>  <span class="cm">// appears HERE</span>
    return result;
}                            <span class="cm">// gone HERE</span></div>
    <div class="analogy">result doesn't have a permanent home anywhere. It's created fresh, on top of the stack, the instant add() is called — and thrown away the instant add() returns.</div>
    <div class="widget">
      <div class="stackwidget" id="resultStack"></div>
      <div class="widget-row" style="margin-top:14px;">
        <button class="btn primary" id="callBtn">Call add(2, 3)</button>
        <button class="btn secondary" id="returnBtn">Return from add()</button>
      </div>
    </div>
    <p class="lede" id="resultLine">Click "Call add(2, 3)" to see result appear.</p>
  `;
  const stackEl = root.querySelector('#resultStack');
  const line = root.querySelector('#resultLine');
  const callBtn = root.querySelector('#callBtn');
  const returnBtn = root.querySelector('#returnBtn');
  callBtn.onclick = () => {
    stackEl.innerHTML = '';
    const p = document.createElement('div');
    p.className = 'plate';
    p.textContent = 'result = 5';
    stackEl.appendChild(p);
    line.textContent = 'result now exists — briefly — on the stack.';
  };
  returnBtn.onclick = () => {
    const plates = stackEl.querySelectorAll('.plate');
    plates.forEach(p=>{ p.classList.add('leaving'); setTimeout(()=>p.remove(),240); });
    line.textContent = 'add() returned — result is completely gone. Nothing remembers it existed.';
  };
}

/* ============================================================
   CARD — What Is a Linker Script?
============================================================ */
function buildWhatIsLinker(root){
  root.innerHTML = `
    <div class="eyebrow">CONCEPT 8 OF 16 · DEFINITION</div>
    <h2>What is a linker script, really?</h2>
    <div class="analogy">Think of it as an <b>address book</b>, not a program. It never runs on the CPU, produces no instructions of its own, and does nothing while your chip is powered on. Its only job happens once, at build time.</div>
    <p class="lede"><b>Definition:</b> a linker script (usually named <code>linker.ld</code> or <code>linker.lds</code> — same format, just a naming preference between toolchains) is a plain text file read by the <b>linker</b> program while your project is being built. It tells the linker exactly which physical address to place every piece of your compiled program at.</p>
    <p class="lede">Without one, the linker has no idea your chip even exists — it doesn't know FLASH starts at a particular address, or how big RAM is. <b>Every different chip needs this information spelled out</b>, because every chip's memory map is different.</p>
    <div class="analogy" style="border-left-color:var(--teal);">One sentence to remember it by: <b>a linker script decides WHERE things go. It never decides WHAT happens while the program runs — that's startup.S's job, coming up next.</b></div>
  `;
}

/* ============================================================
   CARD — Linker Script: Every Building Block
============================================================ */
function buildLinkerGlossary(root){
  root.innerHTML = `
    <div class="eyebrow">CONCEPT 9 OF 16 · REFERENCE</div>
    <h2>linker.lds: every building block, defined</h2>
    <p class="lede">Everything you'll ever need to write a simple linker script comes down to these pieces. Come back to this screen any time you're writing your own.</p>
    <div id="linkerGlossList"></div>
  `;
  const terms = [
    ['MEMORY { }', 'The block that declares which physical memory regions actually exist on the chip — usually just FLASH and RAM.'],
    ['FLASH, RAM', '(names you choose) These aren\'t keywords — they\'re labels you invent. You could call them anything; FLASH and RAM are just the conventional names.'],
    ['(rx) / (rwx)', 'Permission flags on a region: r = readable, w = writable, x = executable. FLASH is usually (rx) — code can run from it, but nothing writes to it at runtime. RAM is (rwx) — fully writable.'],
    ['ORIGIN = 0x...', 'The starting address of a region. This number comes from the chip\'s datasheet — you never invent it.'],
    ['LENGTH = 128K', 'The size of a region. Linker scripts understand K (kilobytes) and M (megabytes) directly.'],
    ['ENTRY(name)', 'Tells the linker (and any debugger) which label is the program\'s true starting point — must exactly match a label startup.S actually defines.'],
    ['SECTIONS { }', 'The block that decides where each kind of compiled data — code, constants, variables — actually lands inside the regions declared above.'],
    ['.  (the dot)', 'A special symbol meaning "the current address, right now, as the linker lays things out." Used to mark a position, e.g. <code>_bss_start = .;</code> means "remember wherever we\'ve reached as _bss_start."'],
    ['*(.text*)', 'A wildcard pattern: the first * means "from every object file"; .text* means "any section whose name starts with .text." Together: "grab the .text section from every file in the project."'],
    ['> FLASH', '"Place this section inside the FLASH region."'],
    ['> RAM AT > FLASH', '"This section\'s working copy lives in RAM, but also keep a permanently stored copy in FLASH" — this is exactly the .data situation from earlier.'],
    ['name = expr;', 'Defines a new symbol — a named address or value the linker calculates once. Other files (like startup.S) can then refer to it by name.'],
    ['ORIGIN(RAM), LENGTH(RAM)', 'Functions you can call inside the script to reuse a region\'s own address or size, instead of retyping the number — e.g. <code>_stack_top = ORIGIN(RAM) + LENGTH(RAM);</code>'],
  ];
  const wrap = root.querySelector('#linkerGlossList');
  terms.forEach(([term, def])=>{
    const div = document.createElement('div');
    div.className = 'gloss';
    div.innerHTML = `<div class="term">${term}</div><div class="def">${def}</div>`;
    wrap.appendChild(div);
  });
}

/* ============================================================
   CARD 10 — linker.lds recap
============================================================ */
function buildLinkerRecap(root){
  root.innerHTML = `
    <div class="eyebrow">CONCEPT 10 OF 16</div>
    <h2>linker.lds's whole job, in one sentence</h2>
    <div class="analogy">Every "which box" answer from the last few screens — linker.lds is the file that actually decided them. It never runs on the CPU. It just writes down the plan.</div>
    <div class="codebox">MEMORY
{
  FLASH (rx)  : ORIGIN = 0x00000000, LENGTH = 128K
  RAM   (rwx) : ORIGIN = 0x80000000, LENGTH = 32K
}
SECTIONS
{
  .text   : { *(.text*) *(.rodata*) }  <span class="hl">> FLASH</span>       <span class="cm">// add(), MAX</span>
  .data   : { ... }  <span class="hl">> RAM AT > FLASH</span>                <span class="cm">// counter</span>
  .bss    : { ... }  <span class="hl">> RAM</span>                          <span class="cm">// total</span>
  _stack_top = ORIGIN(RAM) + LENGTH(RAM);                    <span class="cm">// the stack</span>
}</div>
    <p class="lede">Every single thing you clicked through above — this file is where that decision actually gets made.</p>
  `;
}

/* ============================================================
   CARD — What Is a .S File?
============================================================ */
function buildWhatIsSFile(root){
  root.innerHTML = `
    <div class="eyebrow">CONCEPT 11 OF 16 · DEFINITION</div>
    <h2>What is a .S file, really?</h2>
    <div class="analogy">Unlike a linker script — a paper plan that never runs — a <b>.S file is a real, running program</b>. It's just written in assembly language instead of C.</div>
    <p class="lede"><b>Definition:</b> a <code>.S</code> file is assembly language source code. Each line is (almost always) one direct CPU instruction — far more literal than C, with no automatic bookkeeping done for you. The <b>assembler</b> turns it into a real <code>.o</code> object file, exactly like a compiled C file.</p>
    <p class="lede"><b>Why the very first startup code has to be assembly, not C:</b> the instructions that run immediately after reset must work before the stack even exists. But C code always assumes a working stack is already there — every local variable, every function call depends on it. Assembly is the only language low-level enough to build that foundation starting from literally nothing.</p>
    <div class="analogy" style="border-left-color:var(--teal);">Naming note: you'll see this file called <code>startup.S</code>, <code>crt0.S</code> ("C runtime, file 0"), or <code>vectors.S</code> depending on the toolchain — same idea, different vendor conventions. Capital <code>.S</code> (vs lowercase <code>.s</code>) usually means it's allowed to use C preprocessor directives like <code>#ifdef</code>.</div>
  `;
}

/* ============================================================
   CARD — startup.S: Every Instruction Used
============================================================ */
function buildStartupGlossary(root){
  root.innerHTML = `
    <div class="eyebrow">CONCEPT 12 OF 16 · REFERENCE</div>
    <h2>startup.S: every instruction, defined</h2>
    <p class="lede">Two categories: <b>directives</b> talk to the assembler and produce no CPU instruction by themselves; everything else is a real instruction the CPU actually executes.</p>
    <div class="gloss-group-label">DIRECTIVES — FOR THE ASSEMBLER, NOT THE CPU</div>
    <div id="dirList"></div>
    <div class="gloss-group-label">REAL RISC-V INSTRUCTIONS — THE CPU ACTUALLY RUNS THESE</div>
    <div id="insnList"></div>
  `;
  const directives = [
    ['.section NAME', 'e.g. .section .init', '"Put everything that follows into a section called NAME." Matched later by *(.text.init) in linker.lds.'],
    ['.global NAME', 'e.g. .global _start', 'Makes this label visible outside the file, so linker.lds\'s ENTRY(_start) can actually find it. Without this, the label stays private.'],
    ['NAME:', 'e.g. _start:', 'A label — marks this exact address with a name. Does nothing by itself; it\'s just a bookmark other instructions can jump to.'],
  ];
  const instructions = [
    ['li reg, value', '"Load immediate" — put a literal number directly into a register.'],
    ['la reg, symbol', '"Load address" — put the address of a linker-defined symbol (like _stack_top) into a register.'],
    ['lw reg, off(reg2)', '"Load word" — read 4 bytes from RAM at [reg2 + off] into reg.'],
    ['sw reg, off(reg2)', '"Store word" — write reg\'s value into RAM at [reg2 + off].'],
    ['addi reg, reg2, val', '"Add immediate" — reg = reg2 + val.'],
    ['bge reg, reg2, label', '"Branch if greater-or-equal" — jump to label only if reg &gt;= reg2.'],
    ['bltu reg, reg2, label', '"Branch if less-than, unsigned" — jump to label only if reg &lt; reg2.'],
    ['j label', '"Jump" — always jump to label, no condition.'],
    ['call label', 'Jump to a function AND remember how to return afterward — this is a real function call, e.g. call main.'],
    ['csrw csr, reg', '"Control/status register write" — write reg into a special chip-configuration register (cache settings, counters). Very chip-specific.'],
    ['zero', 'Not an instruction — a special register that always reads as the constant 0. Used in sw zero,... to write zeros without loading 0 first.'],
  ];
  const dirWrap = root.querySelector('#dirList');
  directives.forEach(([term, ex, def])=>{
    const div = document.createElement('div');
    div.className = 'gloss';
    div.innerHTML = `<div class="term">${term}<span class="ex">${ex}</span></div><div class="def">${def}</div>`;
    dirWrap.appendChild(div);
  });
  const insnWrap = root.querySelector('#insnList');
  instructions.forEach(([term, def])=>{
    const div = document.createElement('div');
    div.className = 'gloss';
    div.innerHTML = `<div class="term">${term}</div><div class="def">${def}</div>`;
    insnWrap.appendChild(div);
  });
}

/* ============================================================
   CARD 9 — startup.S recap
============================================================ */
function buildStartupRecap(root){
  root.innerHTML = `
    <div class="eyebrow">CONCEPT 13 OF 16</div>
    <h2>startup.S's whole job, in one sentence</h2>
    <div class="analogy">linker.lds only made a plan on paper. Something still has to actually DO the work — set the stack pointer, copy counter, zero total — before main() is safe to run. That something is startup.S.</div>
    <div class="codebox">_start:
    la sp, _stack_top     <span class="cm">// 1. make the stack usable</span>
    ... copy .data loop    <span class="cm">// 2. counter really becomes 5</span>
    ... clear .bss loop    <span class="cm">// 3. total really becomes 0</span>
    call main              <span class="cm">// 4. only NOW is it safe</span></div>
    <p class="lede">Always in this order. main() assumes all of this already happened — skip any one step and main() runs on broken assumptions.</p>
  `;
}

/* ============================================================
   CARD 10 — Full replay, click-paced
============================================================ */
const REPLAY_STEPS = [
  { t:'Power on', d:'RAM is garbage. SP is garbage. Nothing is safe yet.' },
  { t:'PC jumps to _start', d:'The very first instruction of startup.S begins running.' },
  { t:'la sp, _stack_top', d:'Remember Concept 6? This is the exact moment the stack becomes usable.' },
  { t:'Copy .data: FLASH → RAM', d:'Remember Concept 4? This is that copy happening — counter really becomes 5.' },
  { t:'Clear .bss to zero', d:'Remember Concept 5? This is that clear happening — total really becomes 0.' },
  { t:'call main()', d:'Only now — stack ready, counter correct, total correct — is this safe.' },
  { t:'add(counter, MAX) runs', d:'Remember Concept 7? result is born on the stack, used, then gone.' },
  { t:'Program keeps running', d:'counter now holds 105. Every earlier screen was one piece of this exact sequence.' },
];
let replayIdx = 0;
function buildReplay(root){
  replayIdx = 0;
  renderReplay(root);
}
function renderReplay(root){
  const s = REPLAY_STEPS[replayIdx];
  root.innerHTML = `
    <div class="eyebrow">CONCEPT 14 OF 16 · THE FULL PICTURE</div>
    <h2>Now watch it happen in order</h2>
    <p class="lede">Every step below is something you already understand from a screen before this one.</p>
    <div class="widget" style="text-align:center;">
      <div style="font-family:var(--code); font-size:13px; color:var(--teal); margin-bottom:8px;">STEP ${replayIdx+1} OF ${REPLAY_STEPS.length}</div>
      <h3 style="font-size:19px; margin-bottom:10px;">${esc(s.t)}</h3>
      <p style="color:var(--text-1); font-size:13.5px;">${esc(s.d)}</p>
      <div class="widget-row" style="margin-top:20px;">
        <button class="btn secondary" id="replayBack" ${replayIdx===0?'disabled':''}>◀ Previous step</button>
        <button class="btn primary" id="replayNext" ${replayIdx===REPLAY_STEPS.length-1?'disabled':''}>Next step ▶</button>
      </div>
    </div>
  `;
  root.querySelector('#replayNext').onclick = () => { if(replayIdx<REPLAY_STEPS.length-1){ replayIdx++; renderReplay(root); } };
  root.querySelector('#replayBack').onclick = () => { if(replayIdx>0){ replayIdx--; renderReplay(root); } };
}

/* ============================================================
   CARD — Your Turn: A Template to Start From
============================================================ */
function buildTemplate(root){
  root.innerHTML = `
    <div class="eyebrow">CONCEPT 15 OF 16 · YOUR TURN</div>
    <h2>Templates you can actually start writing from</h2>
    <p class="lede">Copy these, then fill in the blanks with your own chip's real numbers from its datasheet.</p>
    <h3 style="margin-top:18px; color:var(--teal);">linker.lds skeleton</h3>
    <div class="codebox">MEMORY
{
  FLASH (rx)  : ORIGIN = &lt;your FLASH start&gt;, LENGTH = &lt;your FLASH size&gt;
  RAM   (rwx) : ORIGIN = &lt;your RAM start&gt;,   LENGTH = &lt;your RAM size&gt;
}
ENTRY(&lt;your entry label&gt;)
SECTIONS
{
  .text  : { *(.text*) *(.rodata*) }                       > FLASH
  .data  : { _data_start=.; *(.data*); _data_end=.; } > RAM AT > FLASH
  .bss   : { _bss_start=.;  *(.bss*);  _bss_end=.; }  > RAM
  _stack_top = ORIGIN(RAM) + LENGTH(RAM);
}</div>
    <h3 style="margin-top:18px; color:var(--purple);">startup.S skeleton</h3>
    <div class="codebox">.section .init
.global &lt;your entry label&gt;
&lt;your entry label&gt;:
    la sp, _stack_top
    la a0, _data_lma
    la a1, _data_start
    <span class="cm">... copy loop until _data_end ...</span>
    la a0, _bss_start
    la a1, _bss_end
    <span class="cm">... zero loop until _bss_end ...</span>
    call main
loop: j loop</div>
    <h3 style="margin-top:18px;">Before you build, check:</h3>
    <div class="checkrow"><span class="tick">✓</span><span>FLASH and RAM's ORIGIN and LENGTH copied exactly from my chip's datasheet.</span></div>
    <div class="checkrow"><span class="tick">✓</span><span>One entry label name, spelled identically in ENTRY(), .global, and the label itself.</span></div>
    <div class="checkrow"><span class="tick">✓</span><span>Every _xxx_start / _xxx_end name matches exactly between both files.</span></div>
    <div class="checkrow"><span class="tick">✓</span><span>startup.S ends with an infinite loop after call main.</span></div>
  `;
}

/* ============================================================
   CARD 11 — Quiz
============================================================ */
const QUIZ = [
  { q:'Why does counter need to be stored in BOTH FLASH and RAM?', opts:['FLASH is faster than RAM','RAM forgets its value at power-off, so FLASH keeps a permanent starting copy','It doesn\'t really — this is a myth'], a:1 },
  { q:'Why doesn\'t FLASH store a "0" for total?', opts:['FLASH can\'t store the number 0','There\'s no value worth permanently storing — the linker just reserves empty space','total is actually stored in FLASH too'], a:1 },
  { q:'Why must the stack pointer be set up before almost anything else in startup.S?', opts:['It looks better first in the file','Because function calls (and even some setup steps) may need a valid stack to work safely','It doesn\'t matter what order it happens in'], a:1 },
];
function buildQuiz(root){
  root.innerHTML = `
    <div class="eyebrow">CONCEPT 16 OF 16 · QUICK CHECK</div>
    <h2>Three questions — no pressure, just check yourself</h2>
    <div id="quizWrap"></div>
  `;
  const wrap = root.querySelector('#quizWrap');
  QUIZ.forEach((item, qi)=>{
    const block = document.createElement('div');
    block.style.marginBottom = '22px';
    block.innerHTML = `<div class="predict"><div class="q">${qi+1}. ${esc(item.q)}</div></div>`;
    const optsWrap = document.createElement('div');
    item.opts.forEach((opt, oi)=>{
      const b = document.createElement('button');
      b.className = 'qopt';
      b.textContent = opt;
      b.onclick = () => {
        optsWrap.querySelectorAll('.qopt').forEach((el,i)=>{
          el.disabled = true;
          if(i===item.a) el.classList.add('correct');
          else if(i===oi) el.classList.add('wrong');
        });
      };
      optsWrap.appendChild(b);
    });
    block.appendChild(optsWrap);
    wrap.appendChild(block);
  });
}

/* ============================================================
   CARD 12 — Summary
============================================================ */
function buildSummary(root){
  root.innerHTML = `
    <div class="eyebrow">YOU'RE DONE</div>
    <h2>What you can now explain</h2>
    <div class="checkrow"><span class="tick">✓</span><span>RAM is numbered storage that forgets at power-off; FLASH is storage that remembers.</span></div>
    <div class="checkrow"><span class="tick">✓</span><span>Code and constants (.text, .rodata) sit permanently in FLASH — nothing to do at start-up.</span></div>
    <div class="checkrow"><span class="tick">✓</span><span>Initialised globals (.data) need two addresses — a stored copy in FLASH, a working copy in RAM — and startup.S copies between them.</span></div>
    <div class="checkrow"><span class="tick">✓</span><span>Uninitialised globals (.bss) are only reserved, never stored — startup.S writes real zeros in.</span></div>
    <div class="checkrow"><span class="tick">✓</span><span>The stack holds local variables, LIFO, and only works because startup.S set the stack pointer first.</span></div>
    <div class="checkrow"><span class="tick">✓</span><span>linker.lds decides addresses on paper; startup.S is the code that actually does the work.</span></div>
    <div class="analogy" style="margin-top:20px;">If any of those feel shaky, use the trail at the top to jump straight back to that concept — nothing here is timed.</div>
  `;
}

/* ============================================================
   CARD REGISTRY + NAVIGATION
============================================================ */
const CARDS = [
  { title:'Welcome', build:buildIntro },
  { title:'What is RAM?', build:buildRam },
  { title:'FLASH vs RAM', build:buildFlash },
  { title:'.text & .rodata', build:buildTextRodata },
  { title:'.data — two homes', build:buildData },
  { title:'.bss — reserved only', build:buildBss },
  { title:'The stack', build:buildStackConcept },
  { title:'Locals on the stack', build:buildStackLocal },
  { title:'What is a linker script?', build:buildWhatIsLinker },
  { title:'linker.lds glossary', build:buildLinkerGlossary },
  { title:'linker.lds recap', build:buildLinkerRecap },
  { title:'What is a .S file?', build:buildWhatIsSFile },
  { title:'startup.S glossary', build:buildStartupGlossary },
  { title:'startup.S recap', build:buildStartupRecap },
  { title:'Full replay', build:buildReplay },
  { title:'Write-your-own template', build:buildTemplate },
  { title:'Quick check', build:buildQuiz },
  { title:'Summary', build:buildSummary },
];

let cardIdx = 0;

function renderTrail(){
  const trail = document.getElementById('trail');
  trail.innerHTML = '';
  CARDS.forEach((c,i)=>{
    const seg = document.createElement('div');
    seg.className = 'trail-seg' + (i<cardIdx?' done':i===cardIdx?' current':'');
    seg.title = c.title;
    seg.onclick = () => { cardIdx = i; renderCard(); };
    trail.appendChild(seg);
  });
  document.getElementById('trailCaption').textContent = `${cardIdx+1} / ${CARDS.length} — ${CARDS[cardIdx].title}`;
}
function renderCard(){
  const root = document.getElementById('cardRoot');
  root.innerHTML = '';
  CARDS[cardIdx].build(root);
  renderTrail();
  document.getElementById('backBtn').disabled = (cardIdx === 0);
  document.getElementById('nextBtn').textContent = (cardIdx === CARDS.length-1) ? 'Restart from the top ↺' : 'Next ▶';
  window.scrollTo({top:0, behavior:'smooth'});
}
function go(dir){
  if(cardIdx === CARDS.length-1 && dir===1){ cardIdx = 0; renderCard(); return; }
  cardIdx = Math.max(0, Math.min(CARDS.length-1, cardIdx+dir));
  renderCard();
}

renderCard();
</script>
</body>
</html>
ram_flash_guided_lesson.html…]()


## END 

======================================================
