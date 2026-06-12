[miro_speaking_warmup.html](https://github.com/user-attachments/files/28892997/miro_speaking_warmup.html)
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Speaking Warm-up · B1+</title>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600&family=Lora:ital,wght@0,600;1,400&display=swap" rel="stylesheet">
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
:root{
  --green:#1D9E75;--green-light:#E1F5EE;--green-mid:#5DCAA5;--green-dark:#0F6E56;
  --text:#1a1a18;--text-muted:#5F5E5A;--text-hint:#888780;
  --border:#e0ddd6;--bg:#f4f2eb;--surface:#ffffff;
  --radius:14px;--radius-sm:8px;
}
html,body{height:100%;margin:0}
body{
  font-family:'Inter',sans-serif;
  background:var(--bg);
  color:var(--text);
  display:flex;
  flex-direction:column;
  align-items:center;
  justify-content:center;
  min-height:100vh;
  padding:2rem 1rem;
  gap:1.5rem;
}

/* Header */
.header{text-align:center}
.chips{display:flex;gap:8px;justify-content:center;margin-bottom:.75rem;flex-wrap:wrap}
.chip{font-size:11px;font-weight:600;letter-spacing:.07em;text-transform:uppercase;padding:4px 12px;border-radius:20px;border:1px solid var(--border);background:var(--surface);color:var(--text-muted)}
.chip.green{background:var(--green-light);color:var(--green-dark);border-color:var(--green-mid)}
h1{font-family:'Lora',serif;font-size:1.4rem;font-weight:600;color:var(--text);margin-bottom:.3rem}
.sub{font-size:13px;color:var(--text-muted)}

/* Timer */
.timer-wrap{display:flex;align-items:center;gap:10px}
.timer-display{font-size:1.5rem;font-weight:600;color:var(--text);min-width:56px;text-align:center;font-variant-numeric:tabular-nums}
.timer-display.warning{color:#E24B4A}
.tbtn{font-family:'Inter',sans-serif;font-size:12px;font-weight:500;padding:6px 14px;border-radius:var(--radius-sm);border:1px solid var(--border);background:var(--surface);color:var(--text-muted);cursor:pointer;transition:all .15s}
.tbtn:hover{background:var(--green-light);color:var(--green-dark);border-color:var(--green-mid)}
.tbtn.running{border-color:#E24B4A;color:#E24B4A}
.tbtn.running:hover{background:#FCEBEB}

/* Progress dots */
.dots{display:flex;gap:8px;justify-content:center}
.dot{width:10px;height:10px;border-radius:50%;background:var(--border);transition:all .2s;cursor:pointer}
.dot.active{background:var(--green);transform:scale(1.2)}
.dot.done{background:var(--green-mid)}

/* Flashcard */
.scene{
  width:100%;
  max-width:560px;
  height:340px;
  perspective:1000px;
  cursor:pointer;
}
.card-inner{
  width:100%;height:100%;
  position:relative;
  transform-style:preserve-3d;
  transition:transform .5s cubic-bezier(.4,0,.2,1);
}
.card-inner.flipped{transform:rotateY(180deg)}
.card-face{
  position:absolute;
  inset:0;
  backface-visibility:hidden;
  -webkit-backface-visibility:hidden;
  border-radius:var(--radius);
  background:var(--surface);
  border:1px solid var(--border);
  display:flex;
  flex-direction:column;
  padding:2rem 2.25rem;
}
.card-back{transform:rotateY(180deg);background:var(--green-light);border-color:var(--green-mid)}

/* Front face */
.card-label{font-size:11px;font-weight:600;letter-spacing:.07em;text-transform:uppercase;color:var(--green);margin-bottom:1rem}
.card-q{font-family:'Lora',serif;font-size:1.15rem;font-weight:600;line-height:1.65;color:var(--text);flex:1}
.card-footer{display:flex;align-items:center;justify-content:space-between;margin-top:1.25rem}
.vocab-row{display:flex;gap:6px;flex-wrap:wrap}
.vtag{font-size:11px;font-weight:500;padding:3px 9px;background:var(--green-light);color:var(--green-dark);border-radius:20px}
.flip-hint{font-size:11px;color:var(--text-hint);display:flex;align-items:center;gap:4px;white-space:nowrap}

/* Back face */
.hint-label{font-size:11px;font-weight:600;letter-spacing:.07em;text-transform:uppercase;color:var(--green-dark);margin-bottom:.75rem}
.hint-text{font-size:14px;color:var(--green-dark);line-height:1.75;flex:1}
.hint-text em{font-style:italic;opacity:.85}
.back-footer{margin-top:1.25rem;font-size:11px;color:var(--green-dark);opacity:.6;text-align:right}

/* Nav buttons */
.nav{display:flex;align-items:center;gap:12px}
.nbtn{font-family:'Inter',sans-serif;font-size:13px;font-weight:500;padding:9px 20px;border-radius:var(--radius-sm);border:1px solid var(--border);background:var(--surface);color:var(--text-muted);cursor:pointer;display:flex;align-items:center;gap:6px;transition:all .15s}
.nbtn:hover{background:var(--green-light);color:var(--green-dark);border-color:var(--green-mid)}
.nbtn:disabled{opacity:.3;cursor:default;pointer-events:none}
.mark-btn{font-family:'Inter',sans-serif;font-size:12px;font-weight:500;padding:8px 16px;border-radius:var(--radius-sm);border:1px solid var(--border);background:var(--surface);color:var(--text-muted);cursor:pointer;transition:all .15s}
.mark-btn.marked{background:var(--green);color:#fff;border-color:var(--green)}
.mark-btn:hover:not(.marked){background:var(--green-light);color:var(--green-dark);border-color:var(--green-mid)}

/* Finish */
.finish{display:none;text-align:center;background:var(--surface);border:1px solid var(--border);border-radius:var(--radius);padding:2rem;max-width:560px;width:100%}
.finish.show{display:block}
.finish h2{font-family:'Lora',serif;font-size:1.2rem;font-weight:600;margin:.75rem 0 .4rem}
.finish p{font-size:13px;color:var(--text-muted)}
.restart{font-family:'Inter',sans-serif;font-size:13px;font-weight:500;padding:9px 22px;border-radius:var(--radius-sm);border:1px solid var(--green);background:var(--green-light);color:var(--green-dark);cursor:pointer;margin-top:1.25rem;transition:all .15s}
.restart:hover{background:var(--green);color:#fff}

/* Arrow SVGs inline */
.arrow{width:16px;height:16px;stroke:currentColor;stroke-width:2;fill:none;stroke-linecap:round;stroke-linejoin:round;flex-shrink:0}
</style>
</head>
<body>

<div class="header">
  <div class="chips">
    <span class="chip green">Warm-up</span>
    <span class="chip green">B1+</span>
    <span class="chip">5 min</span>
    <span class="chip">1-on-1</span>
  </div>
  <h1>Speaking Warm-up</h1>
  <p class="sub">5 discussion questions · click the card to see a language hint</p>
</div>

<!-- Timer -->
<div class="timer-wrap">
  <svg class="arrow" viewBox="0 0 24 24"><circle cx="12" cy="12" r="9"/><polyline points="12 7 12 12 15 15"/></svg>
  <span class="timer-display" id="timer">5:00</span>
  <button class="tbtn" id="tbtn" onclick="toggleTimer()">Start</button>
</div>

<!-- Progress -->
<div class="dots" id="dots"></div>

<!-- Card -->
<div class="scene" id="scene" onclick="flipCard()">
  <div class="card-inner" id="card-inner">
    <div class="card-face">
      <p class="card-label" id="card-label"></p>
      <p class="card-q" id="card-q"></p>
      <div class="card-footer">
        <div class="vocab-row" id="card-tags"></div>
        <span class="flip-hint">
          <svg class="arrow" viewBox="0 0 24 24" style="width:13px;height:13px"><path d="M1 4v6h6M23 20v-6h-6"/><path d="M20.49 9A9 9 0 0 0 5.64 5.64L1 10m22 4l-4.64 4.36A9 9 0 0 1 3.51 15"/></svg>
          flip for hint
        </span>
      </div>
    </div>
    <div class="card-face card-back">
      <p class="hint-label">💡 Language hint</p>
      <p class="hint-text" id="card-hint"></p>
      <p class="back-footer">tap to flip back</p>
    </div>
  </div>
</div>

<!-- Nav -->
<div class="nav">
  <button class="nbtn" id="prev-btn" onclick="go(-1)">
    <svg class="arrow" viewBox="0 0 24 24"><line x1="19" y1="12" x2="5" y2="12"/><polyline points="12 19 5 12 12 5"/></svg>
    Prev
  </button>
  <button class="mark-btn" id="mark-btn" onclick="markDone()">Mark as discussed</button>
  <button class="nbtn" id="next-btn" onclick="go(1)">
    Next
    <svg class="arrow" viewBox="0 0 24 24"><line x1="5" y1="12" x2="19" y2="12"/><polyline points="12 5 19 12 12 19"/></svg>
  </button>
</div>

<!-- Finish -->
<div class="finish" id="finish">
  <div style="font-size:2rem">🎉</div>
  <h2>All questions discussed!</h2>
  <p>Great warm-up. Time to move on to the main lesson.</p>
  <button class="restart" onclick="restart()">Start again</button>
</div>

<script>
const QS=[
  {
    label:"Question 1 of 5",
    q:"Think about a skill you have — something you're good at. How did you develop it? What would you estimate was the most vital part of that process?",
    tags:["develop","vital","estimate"],
    hint:"Try: "I'd estimate it took me about… / The most vital thing was… / My skills evolved gradually through…""
  },
  {
    label:"Question 2 of 5",
    q:"Have you ever had to convince someone to change their mind about something? What was the situation — and what finally led to them agreeing with you?",
    tags:["convince","lead to","assumption"],
    hint:"Try: "I had to convince… / What eventually led to a change was… / My assumption was that…""
  },
  {
    label:"Question 3 of 5",
    q:"Is there something in your life or city that you consider a nuisance — not dangerous, just annoying? Could it potentially evolve into something more hazardous?",
    tags:["nuisance","hazardous","evolve","potentially"],
    hint:"Try: "It's more of a nuisance than a real problem… / I fear it could evolve into… / It's not hazardous yet, but…""
  },
  {
    label:"Question 4 of 5",
    q:"What's a concept that you find difficult to explain to other people — something from your job, hobby, or area of interest? How would you describe it simply?",
    tags:["concept","refer to","considerably"],
    hint:"Try: "The concept of… is hard to explain because… / I often refer to it as… / It's considerably more complex than it looks…""
  },
  {
    label:"Question 5 of 5",
    q:"If you could make one considerable change to make your city or neighbourhood more habitable, what would it be? Does the problem feel insurmountable, or potentially fixable?",
    tags:["considerably","habitable","insurmountable","potentially"],
    hint:"Try: "I'd considerably improve… / It would make the area more habitable if… / The challenge feels potentially insurmountable because…""
  }
];

let cur=0,done=new Set(),flipped=false,timerOn=false,secs=300,iv=null;

function render(){
  const q=QS[cur];
  document.getElementById('card-label').textContent=q.label;
  document.getElementById('card-q').textContent=q.q;
  document.getElementById('card-hint').textContent=q.hint;
  document.getElementById('card-tags').innerHTML=q.tags.map(t=>`<span class="vtag">${t}</span>`).join('');
  document.getElementById('prev-btn').disabled=cur===0;
  document.getElementById('next-btn').disabled=cur===QS.length-1;
  const mb=document.getElementById('mark-btn');
  mb.textContent=done.has(cur)?'Discussed ✓':'Mark as discussed';
  mb.className='mark-btn'+(done.has(cur)?' marked':'');
  if(flipped){document.getElementById('card-inner').classList.remove('flipped');flipped=false;}
  renderDots();
  document.getElementById('finish').className='finish'+(done.size===QS.length?' show':'');
}

function renderDots(){
  document.getElementById('dots').innerHTML=QS.map((_,i)=>{
    let cls='dot';
    if(i===cur)cls+=' active';
    else if(done.has(i))cls+=' done';
    return`<div class="${cls}" onclick="event.stopPropagation();jump(${i})" title="Question ${i+1}"></div>`;
  }).join('');
}

function flipCard(){
  flipped=!flipped;
  document.getElementById('card-inner').classList.toggle('flipped',flipped);
}
function go(d){cur=Math.max(0,Math.min(QS.length-1,cur+d));render();}
function jump(i){cur=i;render();}
function markDone(){done.has(cur)?done.delete(cur):done.add(cur);render();}
function restart(){done.clear();cur=0;render();document.getElementById('finish').className='finish';}

function toggleTimer(){
  if(timerOn){
    clearInterval(iv);timerOn=false;
    const b=document.getElementById('tbtn');b.textContent='Resume';b.classList.remove('running');
  } else {
    if(secs<=0){secs=300;document.getElementById('timer').textContent='5:00';document.getElementById('timer').classList.remove('warning');}
    timerOn=true;
    const b=document.getElementById('tbtn');b.textContent='Pause';b.classList.add('running');
    iv=setInterval(()=>{
      secs--;
      const m=Math.floor(secs/60),s=secs%60;
      const el=document.getElementById('timer');
      el.textContent=`${m}:${s.toString().padStart(2,'0')}`;
      if(secs<=60)el.classList.add('warning');
      if(secs<=0){
        clearInterval(iv);timerOn=false;
        const b=document.getElementById('tbtn');b.textContent='Done';b.disabled=true;b.classList.remove('running');
      }
    },1000);
  }
}

render();
</script>
</body>
</html>
