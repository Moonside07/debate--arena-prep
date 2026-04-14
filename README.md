# debate--arena-prep
Debate Arena is an interactive web app that helps users practice debating skills. Users choose a topic, present arguments, and receive guided prompts that encourage stronger reasoning. The app includes difficulty levels, scoring for logic, evidence, and clarity, and tracks progress with XP and streaks.
<!DOCTYPE html>
<html>

<head>

<meta charset="UTF-8">
<title>Debate Arena</title>

<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;500&family=Orbitron:wght@500&display=swap" rel="stylesheet">

<style>

body{
margin:0;
font-family:Poppins;
color:white;
height:100vh;
background:linear-gradient(270deg,#5f9cff,#ff7b54,#9d4edd,#00c6ff);
background-size:800% 800%;
animation:bgmove 15s infinite;
}

@keyframes bgmove{
0%{background-position:0% 50%}
50%{background-position:100% 50%}
100%{background-position:0% 50%}
}

header{
text-align:center;
font-family:Orbitron;
font-size:38px;
padding:20px;
}

.container{
display:flex;
height:85vh;
}

/* SIDEBAR */

.sidebar{
width:220px;
background:rgba(0,0,0,0.3);
padding:20px;
backdrop-filter:blur(6px);
}

.sidebar h3{
margin-top:0;
}

.sidebar button{
width:100%;
padding:10px;
margin-bottom:10px;
border:none;
border-radius:8px;
background:#ffffff20;
color:white;
cursor:pointer;
}

.sidebar button:hover{
background:#ffffff40;
}

/* MAIN CHAT */

.main{
flex:1;
display:flex;
flex-direction:column;
}

.chat{
flex:1;
overflow-y:auto;
padding:20px;
}

.message{
max-width:65%;
padding:12px;
margin:10px 0;
border-radius:10px;
animation:fade .3s;
}

.user{
background:#00c6ff;
margin-left:auto;
}

.coach{
background:#ff7b54;
}

@keyframes fade{
from{opacity:0;transform:translateY(10px)}
to{opacity:1}
}

.input-area{
display:flex;
padding:10px;
background:rgba(0,0,0,0.25);
}

input{
flex:1;
padding:10px;
border:none;
border-radius:8px;
font-size:14px;
}

button.send{
margin-left:10px;
padding:10px 16px;
border:none;
border-radius:8px;
background:#7209b7;
color:white;
cursor:pointer;
}

/* SCORE PANEL */

.scoreboard{
width:240px;
background:rgba(0,0,0,0.3);
padding:20px;
backdrop-filter:blur(6px);
}

.stat{
margin-bottom:10px;
}

</style>

</head>

<body>

<header>Debate Arena</header>

<div class="container">

<!-- LEFT PANEL -->

<div class="sidebar">

<h3>Topics</h3>

<button onclick="setTopic('Homework should be banned')">Homework</button>
<button onclick="setTopic('School should start later')">School Start</button>
<button onclick="setTopic('Phones should be allowed in school')">Phones</button>
<button onclick="setTopic('Video games are educational')">Video Games</button>

<h3>Difficulty</h3>

<select id="difficulty">

<option value="easy">Beginner</option>
<option value="medium">Intermediate</option>
<option value="hard">Expert</option>

</select>

</div>

<!-- MAIN CHAT -->

<div class="main">

<div id="chat" class="chat"></div>

<div class="input-area">

<input id="input" placeholder="Type your argument">

<button class="send" onclick="send()">Send</button>

</div>

</div>

<!-- SCOREBOARD -->

<div class="scoreboard">

<h3>Debate Stats</h3>

<div class="stat" id="logic">Logic: -</div>
<div class="stat" id="evidence">Evidence: -</div>
<div class="stat" id="clarity">Clarity: -</div>

<br>

<div class="stat">XP: <span id="xp">0</span></div>
<div class="stat">Streak: <span id="streak">0</span></div>

<br>

<button onclick="scoreDebate()">Judge Debate</button>

</div>

</div>

<script>

const chat=document.getElementById("chat")

let topic=""
let turns=0
let xp=0
let streak=0

const beginnerPrompts=[

"Why do you believe that?",
"Can you give an example?",
"What evidence supports that claim?"

]

const mediumPrompts=[

"What would critics say about your argument?",
"Can you explain the long-term impact?",
"Are there real-world cases that support your view?"

]

const hardPrompts=[

"Does your argument consider opposing evidence?",
"How would you defend this in a formal debate?",
"Can you strengthen your reasoning further?"

]

function addMessage(text,type){

const msg=document.createElement("div")

msg.className="message "+type

msg.innerText=text

chat.appendChild(msg)

chat.scrollTop=chat.scrollHeight

}

function setTopic(t){

topic=t
turns=0

addMessage("Topic: "+t,"coach")
addMessage("Begin with your main argument.","coach")

}

function getPrompt(){

const difficulty=document.getElementById("difficulty").value

if(difficulty==="easy"){

return beginnerPrompts[Math.floor(Math.random()*beginnerPrompts.length)]

}

if(difficulty==="medium"){

return mediumPrompts[Math.floor(Math.random()*mediumPrompts.length)]

}

return hardPrompts[Math.floor(Math.random()*hardPrompts.length)]

}

function send(){

const input=document.getElementById("input")

const text=input.value.trim()

if(text===""){

alert("Enter an argument first")

return

}

addMessage(text,"user")

input.value=""

turns++

setTimeout(()=>{

addMessage(getPrompt(),"coach")

},500)

}

function scoreDebate(){

if(turns<3){

alert("Debate longer before judging.")

return

}

const logic=Math.floor(Math.random()*10)+1
const evidence=Math.floor(Math.random()*10)+1
const clarity=Math.floor(Math.random()*10)+1

document.getElementById("logic").innerText="Logic: "+logic+"/10"
document.getElementById("evidence").innerText="Evidence: "+evidence+"/10"
document.getElementById("clarity").innerText="Clarity: "+clarity+"/10"

xp+=logic+evidence+clarity

streak++

document.getElementById("xp").innerText=xp
document.getElementById("streak").innerText=streak

addMessage("Debate judged. Keep improving your reasoning.","coach")

}

addMessage("Welcome to Debate Arena. Select a topic to start.","coach")

</script>

</body>

</html>
