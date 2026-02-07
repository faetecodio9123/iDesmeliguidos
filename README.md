# idesmeliguidos 
Site para guardar minha memórias do 9° ano com amigos 

<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<title>iDesmeliguidos</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
:root{
  --roxo:#6a2cff;
  --azul:#1fd1ff;
  --rosa:#ff4fd8;
  --verde:#00ff9c;
  --amarelo:#ffe066;
}

*{box-sizing:border-box;font-family:Verdana}

body{
  margin:0;
  min-height:100vh;
  background:
    repeating-linear-gradient(
      45deg,
      rgba(255,255,255,.04),
      rgba(255,255,255,.04) 10px,
      transparent 10px,
      transparent 20px
    ),
    linear-gradient(135deg,var(--rosa),var(--roxo),var(--azul));
  background-attachment:fixed;
  overflow-x:hidden;
}

/* LOGIN */
#login{
  position:fixed;inset:0;
  display:flex;align-items:center;justify-content:center;
  background:#000;z-index:9999;
}
#login .box{
  background:#fff;
  padding:30px;
  border-radius:30px;
  text-align:center;
  box-shadow:0 0 40px #fff6;
}

/* NAV */
nav{
  display:flex;
  flex-wrap:wrap;
  gap:14px;
  padding:16px;
  justify-content:center;
}
nav button{
  border:none;
  padding:14px 26px;
  border-radius:40px;
  background:linear-gradient(135deg,var(--verde),var(--amarelo));
  font-weight:bold;
  font-size:15px;
  cursor:pointer;
  box-shadow:0 8px 0 #0003,0 0 20px #fff4;
  transition:.2s;
}
nav button:hover{transform:translateY(-4px) rotate(-2deg)}
nav button.extras{background:linear-gradient(135deg,var(--rosa),var(--azul))}

/* SECTIONS */
section{display:none;padding:18px}
section.active{display:block}

/* CARD */
.card{
  background:#fff;
  border-radius:40px;
  padding:26px;
  box-shadow:
    0 0 40px rgba(255,255,255,.4),
    inset 0 0 0 6px #fff;
  position:relative;
}

/* STICKERS */
.sticker{
  position:absolute;
  font-size:28px;
  opacity:.9;
}
.s1{top:-14px;left:20px}
.s2{top:-18px;right:30px}
.s3{bottom:-16px;right:40px}

/* HOME */
#homeHeader{text-align:center;margin-bottom:16px}
#homeHeader h1{
  font-size:42px;
  background:linear-gradient(90deg,var(--rosa),var(--azul));
  -webkit-background-clip:text;
  color:transparent;
}
#home video{
  width:100%;
  border-radius:30px;
  box-shadow:0 0 25px #0004;
}

#fakeComments{
  margin-top:16px;
  height:180px;
  overflow:hidden;
  position:relative;
}

.fakeMsg{
  background:#000c;
  color:#fff;
  padding:8px 14px;
  border-radius:20px;
  margin:6px 0;
  animation:rise 6s linear forwards;
  width:fit-content;
}

@keyframes rise{
  from{transform:translateY(160px)}
  to{transform:translateY(-160px);opacity:0}
}

/* GRID */
.grid{
  display:grid;
  gap:14px;
  margin-top:14px;
}
.grid img,.grid video{
  width:100%;
  border-radius:24px;
  box-shadow:0 0 14px #0004;
}

/* CHAT */
.chatMsg{
  background:#eee;
  padding:8px 14px;
  border-radius:18px;
  margin:4px 0;
}

/* EXTRAS */
.extraTabs{
  display:flex;
  flex-wrap:wrap;
  gap:10px;
  justify-content:center;
}
.extraTabs button{
  background:linear-gradient(135deg,var(--azul),var(--verde));
  border:none;
  border-radius:30px;
  padding:12px 20px;
  font-weight:bold;
  cursor:pointer;
}
#moods button{
  font-size:28px;
  background:none;
  border:none;
  cursor:pointer;
}

/* SECRET */
#secret .card{
  background:linear-gradient(135deg,#111,#333);
  color:#fff;
}
canvas{
  background:#fff;
  border-radius:24px;
  border:5px dashed var(--rosa);
}
.clearBtn{
  background:var(--rosa);
  font-weight:bold;
}
</style>
</head>

<body>

<div id="login">
  <div class="box">
    <h2>🔒 iDesmeliguidos</h2>
    <input id="senha" placeholder="Senha do site">
    <br><br>
    <button onclick="entrar()">Entrar</button>
  </div>
</div>

<nav>
  <button onclick="show('home')">Home</button>
  <button onclick="show('episodios')">Episódios</button>
  <button onclick="show('memorias')">Memórias</button>
  <button onclick="show('comentarios')">Comentários</button>
  <button class="extras" onclick="show('extras')">Extras</button>
  <button onclick="showSecret()">🔐</button>
</nav>

<section id="home" class="active">
  <div class="card">
    <div class="sticker s1">⭐</div>
    <div class="sticker s2">🎮</div>
    <div class="sticker s3">💥</div>

    <div id="homeHeader">
      <h1>iDesmeliguidos</h1>
      <p>Amizade, caos e comentários que ninguém pediu.</p>
    </div>

    <video controls></video>
    <div id="fakeComments"></div>
  </div>
</section>

<section id="episodios">
  <div class="card">
    <h2>Episódios</h2>
    <input type="file" accept="video/*,image/*" onchange="addEp(this)">
    <div id="eps" class="grid"></div>
  </div>
</section>

<section id="memorias">
  <div class="card">
    <h2>Memórias</h2>
    <input type="file" id="memFile" accept="image/*,video/*">
    <input id="memText" placeholder="Texto">
    <button onclick="saveMem()">Salvar</button>
    <div id="memList" class="grid"></div>
  </div>
</section>

<section id="comentarios">
  <div class="card">
    <h2>Chat real</h2>
    <input id="user" placeholder="Nome">
    <input id="msg" placeholder="Mensagem">
    <button onclick="sendMsg()">Enviar</button>
    <div id="chat"></div>
  </div>
</section>

<section id="extras">
  <div class="card">
    <div class="extraTabs">
      <button onclick="extra('bv')">Brilhante Victória</button>
      <button onclick="extra('hd')">Henry Danger</button>
      <button onclick="extra('th')">The Thundermans</button>
      <button onclick="extra('sc')">Sam & Cat</button>
    </div>
    <div id="extraContent"></div>
  </div>
</section>

<section id="secret">
  <div class="card">
    <h2>Área Secreta</h2>
    <input id="smsg" placeholder="Mensagem secreta">
    <button onclick="sendSecret()">Enviar</button>
    <div id="secretChat"></div>
    <br>
    <canvas id="draw" width="300" height="300"></canvas>
    <button class="clearBtn" onclick="ctx.clearRect(0,0,300,300)">Limpar desenho</button>
  </div>
</section>

<script>
const SENHA="iDesmeliguidos123";
const SECRETA="JPWMLNFJ";

function entrar(){ if(senha.value===SENHA) login.style.display="none"; }
function show(id){
  document.querySelectorAll("section").forEach(s=>s.classList.remove("active"));
  document.getElementById(id).classList.add("active");
}
function showSecret(){
  if(prompt("Senha secreta:")===SECRETA) show("secret");
}

/* EPISÓDIOS */
function addEp(i){
  const f=i.files[0],u=URL.createObjectURL(f);
  eps.innerHTML+=f.type.startsWith("video")
   ?`<video src="${u}" controls></video>`
   :`<img src="${u}">`;
}

/* MEMÓRIAS */
function saveMem(){
  const f=memFile.files[0],t=memText.value;
  if(f){
    const u=URL.createObjectURL(f);
    memList.innerHTML+=f.type.startsWith("video")
     ?`<video src="${u}" controls></video>`
     :`<img src="${u}">`;
  }
  if(t) memList.innerHTML+=`<p>${t}</p>`;
  memText.value="";
}

/* CHAT REAL */
function sendMsg(){
  chat.innerHTML+=`<div class="chatMsg"><b>${user.value}:</b> ${msg.value}</div>`;
  msg.value="";
}

/* CHAT SECRETO */
function sendSecret(){
  secretChat.innerHTML+=`<div class="chatMsg">${smsg.value}</div>`;
  smsg.value="";
}

/* CHAT FAKE COM BRIGAS */
const fakeUsers=[
  "N1njaBR","FaZeLeo","GG_Master","XP_God","NoScopeX",
  "MrBeastado","Cellbitado","Alanzokaa","GaulesFPS",
  "PlayerZero","ConsoleKing","MobileLenda","iFan2000"
];

const fakeTexts=[
  "isso é fake",
  "para de chorar",
  "aprende a jogar",
  "mentira",
  "MOD????",
  "ninguém liga",
  "tá errado isso",
  "KKKKKK",
  "calma aí",
  "viajou demais"
];

let lastUser=null;

setInterval(()=>{
  const user=fakeUsers[Math.floor(Math.random()*fakeUsers.length)];
  const text=fakeTexts[Math.floor(Math.random()*fakeTexts.length)];

  const d=document.createElement("div");
  d.className="fakeMsg";

  if(Math.random()<0.4 && lastUser){
    d.textContent=user+" → "+lastUser+": "+text;
  }else{
    d.textContent=user+": "+text;
    lastUser=user;
  }

  fakeComments.appendChild(d);
},900);

/* EXTRAS */
let points=0;
function extra(x){
  if(x==="bv"){
    extraContent.innerHTML=`<h3>Como você está hoje?</h3><div id="moods"></div><p id="moodResult"></p>`;
    "😍 🤣 😁 😐 🤨 😶‍🌫️ 🥵 🥶 💩 🤡 🫦".split(" ").forEach(e=>{
      moods.innerHTML+=`<button onclick="moodResult.textContent='Hoje você está: ${e}'">${e}</button>`;
    });
  }
  if(x==="hd"){
    points++;
    extraContent.innerHTML=`Missão do dia: Faça alguém sorrir<br>Pontos: ${points}`;
  }
  if(x==="th"){
    const p=["Super força","Invisibilidade","Telepatia","Velocidade"];
    extraContent.innerHTML=`Poder do dia: ${p[Math.random()*p.length|0]}`;
  }
  if(x==="sc"){
    const caos=["EU GRITEI","CADE O BOTÃO","BANANA CÓSMICA","SOCORRO"];
    extraContent.innerHTML=caos[Math.random()*caos.length|0];
  }
}

/* CANVAS */
let ctx=draw.getContext("2d"),d=false;
draw.onpointerdown=()=>d=true;
draw.onpointerup=()=>d=false;
draw.onpointermove=e=>{if(d)ctx.fillRect(e.offsetX,e.offsetY,4,4);}
</script>

</body>
</html>
