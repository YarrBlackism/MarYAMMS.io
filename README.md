<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Maryam Mood Predictor 💜</title>
<style>
  :root{
    --purple-deep:#3b1160;
    --purple-mid:#5b2a8c;
    --purple-glow:#a86ae8;
    --pink:#ff8fd8;
    --gold:#ffd76e;
    --cream:#fff3fb;
  }
  *{margin:0;padding:0;box-sizing:border-box;}
  html,body{height:100%;}
  body{
    font-family:"Segoe UI",system-ui,-apple-system,sans-serif;
    background:radial-gradient(ellipse at 50% 30%, var(--purple-mid) 0%, var(--purple-deep) 65%, #240a3f 100%);
    overflow:hidden;
    color:var(--cream);
    display:flex;
    align-items:center;
    justify-content:center;
  }

  /* ------- floating hearts ------- */
  .heart{
    position:fixed;
    bottom:-60px;
    font-size:24px;
    animation:floatUp linear infinite;
    opacity:.75;
    pointer-events:none;
    z-index:1;
    filter:drop-shadow(0 0 6px rgba(255,143,216,.6));
  }
  @keyframes floatUp{
    0%{transform:translateY(0) translateX(0) rotate(0deg);opacity:0;}
    10%{opacity:.8;}
    50%{transform:translateY(-55vh) translateX(30px) rotate(20deg);}
    100%{transform:translateY(-115vh) translateX(-30px) rotate(-20deg);opacity:0;}
  }

  /* ------- main card ------- */
  .card{
    position:relative;
    z-index:5;
    width:min(560px,92vw);
    text-align:center;
    background:rgba(255,255,255,.07);
    border:1px solid rgba(255,255,255,.18);
    border-radius:28px;
    padding:36px 28px 44px;
    backdrop-filter:blur(10px);
    box-shadow:0 20px 60px rgba(0,0,0,.45), inset 0 1px 0 rgba(255,255,255,.15);
  }
  h1{
    font-size:clamp(1.5rem,5vw,2.2rem);
    letter-spacing:.5px;
    margin-bottom:6px;
    background:linear-gradient(90deg,var(--pink),var(--gold),var(--pink));
    background-size:200% auto;
    -webkit-background-clip:text;
    background-clip:text;
    color:transparent;
    animation:shine 4s linear infinite;
  }
  @keyframes shine{to{background-position:200% center;}}
  .subtitle{color:var(--purple-glow);font-size:.95rem;margin-bottom:26px;}

  button{
    font-family:inherit;
    cursor:pointer;
    border:none;
    border-radius:999px;
    font-weight:700;
    transition:transform .15s ease, box-shadow .15s ease;
  }
  button:active{transform:scale(.96);}

  .big-btn{
    font-size:1.15rem;
    padding:16px 38px;
    color:#3b1160;
    background:linear-gradient(135deg,var(--gold),var(--pink));
    box-shadow:0 8px 24px rgba(255,143,216,.4);
  }
  .big-btn:hover{transform:translateY(-3px);box-shadow:0 12px 30px rgba(255,143,216,.55);}

  .machine-label{
    display:inline-block;
    font-size:.8rem;
    letter-spacing:2px;
    text-transform:uppercase;
    color:var(--gold);
    border:1px dashed rgba(255,215,110,.5);
    border-radius:999px;
    padding:4px 14px;
    margin-bottom:18px;
  }

  /* ------- slot machine ------- */
  .slot{
    width:min(340px,80vw);
    margin:0 auto 24px;
    background:linear-gradient(#2a0b4a,#1c0733);
    border:3px solid var(--gold);
    border-radius:18px;
    padding:14px;
    box-shadow:0 0 30px rgba(255,215,110,.25), inset 0 0 20px rgba(0,0,0,.6);
  }
  .slot-window{
    height:80px;
    overflow:hidden;
    border-radius:10px;
    background:rgba(255,255,255,.06);
    position:relative;
  }
  .slot-window::before,.slot-window::after{
    content:"";position:absolute;left:0;right:0;height:22px;z-index:2;pointer-events:none;
  }
  .slot-window::before{top:0;background:linear-gradient(#1c0733,transparent);}
  .slot-window::after{bottom:0;background:linear-gradient(transparent,#1c0733);}
  .slot-reel{transition:none;}
  .slot-item{
    height:80px;
    display:flex;
    align-items:center;
    justify-content:center;
    font-size:1.25rem;
    font-weight:800;
  }

  /* ------- wheel ------- */
  .wheel-wrap{
    position:relative;
    width:min(300px,78vw);
    aspect-ratio:1;
    margin:0 auto 24px;
  }
  .pointer{
    position:absolute;
    top:-10px;left:50%;
    transform:translateX(-50%);
    width:0;height:0;
    border-left:14px solid transparent;
    border-right:14px solid transparent;
    border-top:24px solid var(--gold);
    z-index:3;
    filter:drop-shadow(0 3px 4px rgba(0,0,0,.5));
  }
  #wheelSvg{
    width:100%;height:100%;
    border-radius:50%;
    box-shadow:0 0 0 6px var(--gold), 0 0 40px rgba(255,215,110,.3);
    transition:transform 4.5s cubic-bezier(.12,.65,.1,1);
  }

  /* ------- result ------- */
  .mood-result{
    font-size:clamp(1.4rem,5vw,2rem);
    font-weight:800;
    margin:8px 0 4px;
  }
  .mood-emoji{font-size:3.4rem;display:block;margin-bottom:8px;animation:pop .5s ease;}
  @keyframes pop{0%{transform:scale(0);}70%{transform:scale(1.25);}100%{transform:scale(1);}}
  .mood-desc{color:var(--purple-glow);margin-bottom:26px;font-size:.95rem;}

  .choices{display:flex;flex-direction:column;gap:12px;align-items:center;}
  .choice-btn{
    width:min(320px,100%);
    padding:14px 20px;
    font-size:1rem;
    color:var(--cream);
    background:rgba(255,255,255,.1);
    border:1px solid rgba(255,255,255,.25);
  }
  .choice-btn:hover{background:rgba(255,143,216,.2);border-color:var(--pink);transform:translateY(-2px);}

  /* love question */
  .love-q{font-size:1.3rem;font-weight:800;margin-bottom:20px;}
  .love-btns{position:relative;height:150px;}
  .yes-btn{
    padding:14px 44px;font-size:1.1rem;
    color:#3b1160;
    background:linear-gradient(135deg,#7dffb0,var(--gold));
    box-shadow:0 8px 22px rgba(125,255,176,.35);
  }
  .no-btn{
    position:absolute;
    padding:14px 44px;font-size:1.1rem;
    color:var(--cream);
    background:rgba(255,80,110,.85);
    left:calc(50% + 80px);
    top:0;
    transition:left .18s ease, top .18s ease;
  }
  .yes-wrap{position:absolute;left:calc(50% - 160px);top:0;}

  .back-link{
    margin-top:22px;
    background:none;
    color:var(--purple-glow);
    font-size:.85rem;
    text-decoration:underline;
  }

  .big-message{
    font-size:clamp(1.6rem,6vw,2.4rem);
    font-weight:800;
    animation:pop .5s ease;
    line-height:1.3;
  }

  /* falling emoji effects */
  .fall{
    position:fixed;
    top:-50px;
    font-size:30px;
    z-index:50;
    pointer-events:none;
    animation:fallDown linear forwards;
  }
  @keyframes fallDown{
    to{transform:translateY(115vh) rotate(360deg);}
  }

  /* hug */
  .hug-stage{font-size:3.2rem;letter-spacing:8px;}
  .hug-emojis{display:inline-flex;gap:60px;transition:gap 1.4s ease;}
  .hug-emojis.together{gap:2px;}
  .hug-heart{opacity:0;transition:opacity .6s ease .9s;font-size:2rem;vertical-align:middle;}
  .hug-emojis.together + .hug-heart{opacity:1;}

  .hidden{display:none;}

  @media (prefers-reduced-motion: reduce){
    .heart,.fall,h1{animation:none;}
    #wheelSvg{transition:none;}
  }
</style>
</head>
<body>

<div class="card" id="card">

  <!-- START SCREEN -->
  <div id="startScreen">
    <h1>💜 Maryam Mood Predictor 💜</h1>
    <p class="subtitle">Highly scientific. 100% accurate. Do not question the machine.</p>
    <button class="big-btn" onclick="startPrediction()">Predict The Mood ✨</button>
  </div>

  <!-- SLOT MACHINE -->
  <div id="slotScreen" class="hidden">
    <span class="machine-label">🎰 Slot Machine Mode</span>
    <div class="slot">
      <div class="slot-window">
        <div class="slot-reel" id="slotReel"></div>
      </div>
    </div>
    <button class="big-btn" id="slotBtn" onclick="spinSlot()">Pull The Lever 🎰</button>
  </div>

  <!-- WHEEL -->
  <div id="wheelScreen" class="hidden">
    <span class="machine-label">🎡 Wheel Of Maryam Mode</span>
    <div class="wheel-wrap">
      <div class="pointer"></div>
      <svg id="wheelSvg" viewBox="0 0 200 200"></svg>
    </div>
    <button class="big-btn" id="wheelBtn" onclick="spinWheel()">Spin The Wheel 🎡</button>
  </div>

  <!-- RESULT -->
  <div id="resultScreen" class="hidden">
    <span class="mood-emoji" id="moodEmoji"></span>
    <div class="mood-result" id="moodName"></div>
    <p class="mood-desc" id="moodDesc"></p>
    <div class="choices">
      <button class="choice-btn" onclick="showKisses()">Awww sooo cute 😚</button>
      <button class="choice-btn" onclick="showLove()">Do you love me? 🥺</button>
      <button class="choice-btn" onclick="showHug()">Ataaasaaaa 🤗</button>
    </div>
    <button class="back-link" onclick="reset()">↻ predict again</button>
  </div>

  <!-- LOVE QUESTION -->
  <div id="loveScreen" class="hidden">
    <p class="love-q">Do you love me? 🥺👉👈</p>
    <div class="love-btns">
      <div class="yes-wrap"><button class="yes-btn" onclick="loveYes()">YES 💖</button></div>
      <button class="no-btn" id="noBtn">No</button>
    </div>
    <button class="back-link" onclick="backToResult()">← back</button>
  </div>

  <!-- KISSES / YES / HUG MESSAGE -->
  <div id="messageScreen" class="hidden">
    <div class="big-message" id="bigMessage"></div>
    <div id="hugArea" class="hidden" style="margin-top:20px;">
      <div class="hug-stage">
        <span class="hug-emojis" id="hugEmojis"><span>🧍‍♂️</span><span>🧍‍♀️</span></span><span class="hug-heart">💞</span>
      </div>
    </div>
    <button class="back-link" onclick="backToResult()">← back to the mood</button>
  </div>

</div>

<script>
/* ---------------- MOODS ---------------- */
const MOODS = [
  {name:"Angry MarYAM", emoji:"😤", color:"#ff5a6e", desc:"Approach with snacks. Do NOT make eye contact. Apologize even if innocent."},
  {name:"Sad MarYAM", emoji:"🥺", color:"#6ea8ff", desc:"Deploy hugs immediately. Blanket burrito recommended."},
  {name:"Evil MarYAM", emoji:"😈", color:"#a86ae8", desc:"She is plotting something. You will find out too late. Good luck."},
  {name:"Romantic MarYAM", emoji:"🥰", color:"#ff8fd8", desc:"Congratulations!! Enjoy it while it lasts. Say something sweet NOW."},
  {name:"Harami Mode MarYAM", emoji:"😏", color:"#ffd76e", desc:"Chaos level: maximum. Hide your food, hide your phone, trust nothing."},
];
let currentMood = null;

/* ---------------- FLOATING HEARTS ---------------- */
const HEARTS = ["💜","💖","💗","💘","💕","🤍"];
for(let i=0;i<18;i++){
  const h=document.createElement("div");
  h.className="heart";
  h.textContent=HEARTS[Math.floor(Math.random()*HEARTS.length)];
  h.style.left=Math.random()*100+"vw";
  h.style.fontSize=(16+Math.random()*26)+"px";
  h.style.animationDuration=(7+Math.random()*9)+"s";
  h.style.animationDelay=(-Math.random()*14)+"s";
  document.body.appendChild(h);
}

/* ---------------- SCREENS ---------------- */
const screens=["startScreen","slotScreen","wheelScreen","resultScreen","loveScreen","messageScreen"];
function show(id){
  screens.forEach(s=>document.getElementById(s).classList.toggle("hidden",s!==id));
}

/* ---------------- START: pick machine at random ---------------- */
function startPrediction(){
  if(Math.random()<0.5){ setupSlot(); show("slotScreen"); }
  else { setupWheel(); show("wheelScreen"); }
}

/* ---------------- SLOT MACHINE ---------------- */
let slotResultIndex=0;
function setupSlot(){
  const reel=document.getElementById("slotReel");
  reel.style.transition="none";
  reel.style.transform="translateY(0)";
  // build a long strip of moods, repeated
  let html="";
  for(let r=0;r<12;r++){
    MOODS.forEach(m=>{
      html+=`<div class="slot-item" style="color:${m.color}">${m.emoji} ${m.name}</div>`;
    });
  }
  reel.innerHTML=html;
  document.getElementById("slotBtn").disabled=false;
}
function spinSlot(){
  const btn=document.getElementById("slotBtn");
  btn.disabled=true;
  slotResultIndex=Math.floor(Math.random()*MOODS.length);
  const itemH=80;
  // land on an item deep in the strip
  const targetRow=9*MOODS.length+slotResultIndex;
  const reel=document.getElementById("slotReel");
  reel.style.transition="transform 3.6s cubic-bezier(.15,.7,.2,1)";
  reel.style.transform=`translateY(-${targetRow*itemH}px)`;
  setTimeout(()=>finish(MOODS[slotResultIndex]),3900);
}

/* ---------------- WHEEL ---------------- */
let wheelRotation=0;
function setupWheel(){
  const svg=document.getElementById("wheelSvg");
  const n=MOODS.length, cx=100, cy=100, r=100;
  let paths="";
  for(let i=0;i<n;i++){
    const a0=(i/n)*2*Math.PI - Math.PI/2;
    const a1=((i+1)/n)*2*Math.PI - Math.PI/2;
    const x0=cx+r*Math.cos(a0), y0=cy+r*Math.sin(a0);
    const x1=cx+r*Math.cos(a1), y1=cy+r*Math.sin(a1);
    paths+=`<path d="M${cx},${cy} L${x0},${y0} A${r},${r} 0 0 1 ${x1},${y1} Z" fill="${MOODS[i].color}"/>`;
    const mid=(a0+a1)/2;
    const tx=cx+r*0.62*Math.cos(mid), ty=cy+r*0.62*Math.sin(mid);
    paths+=`<text x="${tx}" y="${ty}" font-size="16" text-anchor="middle" dominant-baseline="middle">${MOODS[i].emoji}</text>`;
  }
  paths+=`<circle cx="${cx}" cy="${cy}" r="14" fill="#2a0b4a" stroke="#ffd76e" stroke-width="3"/>`;
  svg.innerHTML=paths;
  wheelRotation=0;
  svg.style.transition="none";
  svg.style.transform="rotate(0deg)";
  document.getElementById("wheelBtn").disabled=false;
}
function spinWheel(){
  const btn=document.getElementById("wheelBtn");
  btn.disabled=true;
  const n=MOODS.length;
  const winner=Math.floor(Math.random()*n);
  const segAngle=360/n;
  // pointer at top; segment i center is at i*seg + seg/2 (from top, clockwise)
  const targetAngle=360*6 + (360 - (winner*segAngle + segAngle/2));
  const svg=document.getElementById("wheelSvg");
  svg.style.transition="transform 4.5s cubic-bezier(.12,.65,.1,1)";
  requestAnimationFrame(()=>{ svg.style.transform=`rotate(${targetAngle}deg)`; });
  setTimeout(()=>finish(MOODS[winner]),4800);
}

/* ---------------- RESULT ---------------- */
function finish(mood){
  currentMood=mood;
  document.getElementById("moodEmoji").textContent=mood.emoji;
  const nameEl=document.getElementById("moodName");
  nameEl.textContent=mood.name+"!";
  nameEl.style.color=mood.color;
  document.getElementById("moodDesc").textContent=mood.desc;
  show("resultScreen");
}
function reset(){ show("startScreen"); }
function backToResult(){ show("resultScreen"); }

/* ---------------- EMOJI RAIN ---------------- */
function rain(emojis,count){
  for(let i=0;i<count;i++){
    setTimeout(()=>{
      const e=document.createElement("div");
      e.className="fall";
      e.textContent=emojis[Math.floor(Math.random()*emojis.length)];
      e.style.left=Math.random()*100+"vw";
      e.style.fontSize=(20+Math.random()*28)+"px";
      e.style.animationDuration=(2.2+Math.random()*2.5)+"s";
      document.body.appendChild(e);
      setTimeout(()=>e.remove(),5200);
    }, i*90);
  }
}

/* ---------------- KISSES ---------------- */
function showKisses(){
  document.getElementById("bigMessage").innerHTML="MWAH MWAH MWAH 😚😚😚<br>Kisses incoming!!";
  document.getElementById("hugArea").classList.add("hidden");
  show("messageScreen");
  rain(["💋","😚","😘","💖"],40);
}

/* ---------------- LOVE ---------------- */
function showLove(){
  show("loveScreen");
  const no=document.getElementById("noBtn");
  no.style.left="calc(50% + 80px)";
  no.style.top="0px";
}
function dodge(){
  const no=document.getElementById("noBtn");
  const area=no.parentElement.getBoundingClientRect();
  const maxX=area.width-no.offsetWidth;
  const maxY=area.height-no.offsetHeight;
  no.style.left=Math.random()*Math.max(maxX,0)+"px";
  no.style.top=Math.random()*Math.max(maxY,0)+"px";
}
const noBtn=document.getElementById("noBtn");
noBtn.addEventListener("mouseenter",dodge);
noBtn.addEventListener("click",dodge);
noBtn.addEventListener("touchstart",e=>{e.preventDefault();dodge();},{passive:false});
function loveYes(){
  document.getElementById("bigMessage").innerHTML="I KNEW IT!! 💖💖💖<br>I love you more!!";
  document.getElementById("hugArea").classList.add("hidden");
  show("messageScreen");
  rain(["💖","💘","💝","🥰","💜"],45);
}

/* ---------------- HUG ---------------- */
function showHug(){
  document.getElementById("bigMessage").innerHTML="ATAAASAAAA!! 🤗<br>Biggest hug ever!!";
  const hugArea=document.getElementById("hugArea");
  hugArea.classList.remove("hidden");
  const emojis=document.getElementById("hugEmojis");
  emojis.classList.remove("together");
  show("messageScreen");
  setTimeout(()=>emojis.classList.add("together"),150);
  rain(["🤗","💞","💜","🫂"],30);
}
</script>
</body>
</html>
