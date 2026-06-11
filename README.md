<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Teste Extremamente Científico</title>
<style>
body{
margin:0;font-family:Arial,sans-serif;
background:#121212;color:white;
display:flex;justify-content:center;align-items:center;
height:100vh;overflow:hidden;
}
.card{
background:#1e1e1e;padding:30px;border-radius:20px;
width:min(90%,700px);text-align:center;
box-shadow:0 0 20px rgba(0,0,0,.4);
}
button{
padding:12px 20px;margin:8px;border:none;border-radius:10px;
cursor:pointer;font-size:16px;
}
.opt{background:#2d2d2d;color:white;}
.main{background:#4f46e5;color:white;}
#gameArea{
position:relative;height:350px;border:2px solid #333;
margin-top:15px;overflow:hidden;border-radius:15px;
}
.target{
position:absolute;width:45px;height:45px;
background:#4f46e5;border-radius:12px;cursor:pointer;
}
.hidden{display:none;}
.bar{
height:18px;background:#333;border-radius:10px;overflow:hidden;
}
.fill{
height:100%;width:0;background:#4f46e5;
}
</style>
</head>
<body>

<div class="card" id="app"></div>

<script>
const app=document.getElementById('app');

function screen1(){
app.innerHTML=`
<h1>Teste Extremamente Científico</h1>
<br><br>
<button class="main" onclick="game()">Iniciar</button>`;
}

let score=0;

function game(){
app.innerHTML=`
<h2>Mini Jogo</h2>
<p>Clique nos quadrados até chegar em 20 pontos.</p>
<p>Pontos: <span id="s">0</span>/20</p>
<div id="gameArea"></div>`;

const area=document.getElementById('gameArea');

function spawn(){
if(score>=20){
prize();
return;
}
let t=document.createElement('div');
t.className='target';
t.style.left=Math.random()*85+'%';
t.style.top=Math.random()*80+'%';
t.onclick=()=>{
score++;
document.getElementById('s').innerText=score;
t.remove();
spawn();
}
area.appendChild(t);
}
spawn();
}

function prize(){
app.innerHTML=`
<h2>Parabéns Ana!!</h2>
<p>Você completou o jogo.</p>
<p>Seu prêmio é responder algumas perguntas.</p>
<button class="main" onclick="q1()">Receber prêmio</button>`;
}

function q1(){
app.innerHTML=`
<h2>Você gosta mais de:</h2>
<button class="opt" onclick="q2()">🐱 Gatos</button>
<button class="opt" onclick="q2()">🐶 Cachorros</button>`;
}

function q2(){
app.innerHTML=`
<h2>Você prefere:</h2>
<button class="opt" onclick="q3()">😴 Dormir</button>
<button class="opt" onclick="q3()">📚 Estudar</button>`;
}

function q3(){
app.innerHTML=`
<h2>Você prefere:</h2>
<button class="opt" onclick="analise()">🏄 Surf</button>
<button class="opt" onclick="analise()">🛹 Skate</button>`;
}

function analise(){
app.innerHTML=`
<h2>Analisando respostas...</h2>
<div class="bar"><div class="fill" id="f"></div></div>
<p id="txt">Inicializando...</p>`;

let p=0;
const msgs=[
"Calculando compatibilidade...",
"Comparando respostas...",
"Executando algoritmos super avançados...",
"Resultado encontrado."
];
let i=0;

let t=setInterval(()=>{
p+=2;
document.getElementById('f').style.width=p+'%';
if(p%25===0 && i<msgs.length){
document.getElementById('txt').innerText=msgs[i++];
}
if(p>=100){
clearInterval(t);
setTimeout(()=>extra(),500);
}
},40);
}

function extra(){
app.innerHTML=`
<h2>Compatibilidade: 99,99%</h2>
<p>Isso foi inesperadamente alto.</p>
<button class="main" onclick="beauty()">Prosseguir</button>`;
}

function beauty(){
let buttons='';
for(let i=0;i<=10;i++){
buttons+=`<button class="opt" onclick="beautyResult(${i})">${i}</button>`;
}
app.innerHTML=`
<h2>Pergunta Extra Obrigatória</h2>
<p>De 0 a 10, quanto você se acha bonita?</p>
${buttons}`;
}

function beautyResult(n){
let msg = n<10
? "Resposta registrada.<br><br>Porém o sistema detectou uma inconsistência.<br>Valor informado: "+n+"<br>Valor correto: acima de 10 😌"
: "Você tá muito certa em, 10 é pouco para te mensurar 😌";

app.innerHTML=`
<h2>Resultado</h2>
<p>${msg}</p>
<button class="main" onclick="experts()">Continuar</button>`;
}

function experts(){
app.innerHTML=`
<h2>Consultando especialistas...</h2>
<p id="e"></p>`;

const lines=[
"Especialista 1: aprovado.",
"Especialista 2: aprovado.",
"Especialista 3: aprovado.",
"Especialista 4: também aprovado.",
"Especialista 5: perguntou por que demorou tanto."
];

let i=0;
const el=document.getElementById('e');

let t=setInterval(()=>{
el.innerHTML += lines[i]+"<br>";
i++;
if(i===lines.length){
clearInterval(t);
setTimeout(finalScreen,1200);
}
},900);
}

function finalScreen(){
app.innerHTML=`
<h2>Relatório Final</h2>

<p>Após diversas análises, o sistema concluiu que:</p>

<h3>Você é exatamene quem eu procuro.</h3>

<p><strong>¡!¿falha¿!¡</strong><br> <br>Sistema não consegue confirma isso.<br>necessario um teste</p>

<p><strong>Teste:</strong> sairmos juntos.</p>

<h3>Ana, você gostaria de sair comigo?</h3>

<button class="main" onclick="yes()">Aceitar teste</button>
<button class="opt" onclick="no()">Recusar teste</button>
`;
}

function yes(){
app.innerHTML=`
<h2>Parabéns 🎉</h2>
<p>Você escolheu o melhor final possível.</p>
<p>Agora só falta a gente marcar o dia 😌</p>`;
}

function no(){
app.innerHTML=`
<h2>Resposta registrada.</h2>
<p>...</p>
<p>Os especialistas solicitaram uma segunda tentativa.</p>
<button class="main" onclick="finalScreen()">Reconsiderar decisão</button>`;
}

screen1();
</script>
</body>
</html>
