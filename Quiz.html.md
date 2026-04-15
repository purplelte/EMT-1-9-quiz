<!DOCTYPE html>  
<html lang="en">  
<head>  
<meta charset="UTF-8">  
<meta name="viewport" content="width=device-width, initial-scale=1.0">  
<meta name="apple-mobile-web-app-capable" content="yes">  
<meta name="theme-color" content="#0a0c10">  
<title>EMT Quiz</title>  
  
<style>  
:root {  
  --bg:#0a0c10;  
  --surface:#111318;  
  --surface2:#181c23;  
  --border:#252a35;  
  --accent:#e8ff47;  
  --accent2:#47c8ff;  
  --danger:#ff4757;  
  --success:#2ed573;  
  --text:#e8eaf0;  
  --muted:#6b7280;  
  --correct-bg:#0d2a1a;  
  --wrong-bg:#2a0d0d;  
}  
  
*{box-sizing:border-box;margin:0;padding:0;}  
  
body{  
  background:var(--bg);  
  color:var(--text);  
  font-family:-apple-system,system-ui;  
  -webkit-tap-highlight-color:transparent;  
}  
  
/* INTRO */  
#intro{  
  height:100vh;  
  display:flex;  
  flex-direction:column;  
  justify-content:center;  
  align-items:center;  
  text-align:center;  
  padding:20px;  
}  
  
.title{  
  font-size:60px;  
  font-weight:800;  
}  
.title span{color:var(--accent);}  
  
.btn{  
  margin-top:40px;  
  padding:18px 50px;  
  font-size:20px;  
  background:var(--accent);  
  border:none;  
  border-radius:10px;  
}  
  
/* QUIZ */  
#quiz{display:none;padding:20px;}  
  
.q-text{  
  font-size:20px;  
  margin-bottom:20px;  
}  
  
.option{  
  background:var(--surface);  
  border:1px solid var(--border);  
  border-radius:12px;  
  padding:18px;  
  margin-bottom:12px;  
  font-size:16px;  
}  
  
.option.selected{border-color:var(--accent2);}  
.option.correct{background:var(--correct-bg);}  
.option.wrong{background:var(--wrong-bg);}  
  
button{  
  min-height:48px;  
  padding:14px;  
  width:100%;  
  margin-top:10px;  
  border:none;  
  border-radius:10px;  
  font-size:16px;  
}  
  
.primary{background:var(--accent);}  
  
/* RESULTS */  
#results{  
  display:none;  
  text-align:center;  
  padding:40px;  
}  
.score{  
  font-size:50px;  
  margin:20px 0;  
}  
</style>  
</head>  
  
<body>  
  
<div id="intro">  
  <div class="title">EMT <span>QUIZ</span></div>  
  <button class="btn" onclick="start()">START</button>  
</div>  
  
<div id="quiz">  
  <div id="progress"></div>  
  <div class="q-text" id="q"></div>  
  <div id="opts"></div>  
  <button class="primary" onclick="check()">CHECK</button>  
  <button onclick="next()">NEXT</button>  
</div>  
  
<div id="results">  
  <h1>Done</h1>  
  <div class="score" id="score"></div>  
  <button onclick="restart()">Restart</button>  
</div>  
  
<script>  
const questions = [  
{q:"EMS stands for?",opts:["Emergency Medical Services","Emergency System","Medical Service","Emergency Support"],a:0},  
{q:"Primary EMT role?",opts:["Diagnose","Transport & care","Surgery","Prescribe"],a:1},  
{q:"Implied consent is for?",opts:["Minors","Unconscious patients","Refusals","Doctors"],a:1},  
{q:"Normal adult RR?",opts:["6-10","12-20","20-30","30-40"],a:1},  
{q:"Shock means?",opts:["Pain","Low BP","Poor perfusion","Unconscious"],a:2}  
];  
  
let i=0,score=0,sel=null;  
  
function start(){  
  document.getElementById("intro").style.display="none";  
  document.getElementById("quiz").style.display="block";  
  render();  
}  
  
function render(){  
  let q=questions[i];  
  document.getElementById("q").textContent=q.q;  
  document.getElementById("progress").textContent=`${i+1}/${questions.length}`;  
  let opts="";  
  q.opts.forEach((o,idx)=>{  
    opts+=`<div class="option" onclick="pick(${idx},this)">${o}</div>`;  
  });  
  document.getElementById("opts").innerHTML=opts;  
  sel=null;  
}  
  
function pick(idx,el){  
  document.querySelectorAll(".option").forEach(o=>o.classList.remove("selected"));  
  el.classList.add("selected");  
  sel=idx;  
}  
  
function check(){  
  if(sel===null)return;  
  let q=questions[i];  
  document.querySelectorAll(".option").forEach((o,idx)=>{  
    if(idx===q.a)o.classList.add("correct");  
    else if(idx===sel)o.classList.add("wrong");  
  });  
  if(sel===q.a)score++;  
}  
  
function next(){  
  i++;  
  if(i>=questions.length){  
    document.getElementById("quiz").style.display="none";  
    document.getElementById("results").style.display="block";  
    document.getElementById("score").textContent=`${score}/${questions.length}`;  
  } else render();  
}  
  
function restart(){  
  i=0;score=0;  
  document.getElementById("results").style.display="none";  
  start();  
}  
</script>  
  
</body>  
</html>  
