Boas vindas ao meu perfil 💙💙
Meu nome é Beatriz 3ºA
Estou estudando na Alura
Estou me desenvolvendo na linguagem JavaScript
Utilizo esse espaço para minha organização e compartilhamento dos meu projetos desenvolvidos






Projeto Ping Pong P5


//variáveis da bolinha
let xBolinha = 300;
let yBolinha = 200;
let diametro = 23;
let raio = diametro / 2 ;

//velocidade da bolinha
let velocidadeXBolinha = 6;
let velocidadeYBolinha = 6;

//variávies da raquete
let xRaquete = 5;
let yRaquete = 150;
let raqueteComprimento = 10;
let raqueteAltura = 90;

//variáveis do oponente
let xRaqueteOponente = 585;
let yRaqueteOponente = 150;
let velocidadeYOponete;

let colidiu = false;

//placar do jogo
let meusPontos = 0;
let pontosDoOponente = 0;

//sons do jogo
let raquetada;
let ponto;
let trilha;

function preload(){
  trilha = loadSound("trilha.mp3");
  ponto = loadSound("ponto.mp3");
  raquetada = loadSound("raquetada.mp3");
}

function setup() {
  createCanvas(600, 400);
  trilha.loop ();
}

function draw() {
  background(0);
mostraBolinha ();
movimentaBolinha();
verificaColisaoBorda();
  mostraRaquete(xRaquete,yRaquete);
  movimentoMinhaRaquete();
  //verificaColisaoRaquete();
  verificaColisaoRaquete(xRaquete, yRaquete);
  mostraRaquete(xRaqueteOponente, yRaqueteOponente);
  movimentaRaqueteOponente();
  verificaColisaoRaquete(xRaqueteOponente, yRaqueteOponente);
  incluirPlacar();
  marcaPonto();

}


function mostraBolinha(){
circle(xBolinha,yBolinha,diametro);  
}

function movimentaBolinha(){
  xBolinha += velocidadeXBolinha;
  yBolinha += velocidadeYBolinha;
}

function verificaColisaoBorda(){
 if (xBolinha + raio> width || 
     xBolinha - raio< 0){
   velocidadeXBolinha *= -1;
 }
if (yBolinha + raio> height || 
    yBolinha - raio< 0){
  velocidadeYBolinha *= -1;
}
}

function mostraRaquete(x,y){
  rect(x, y, raqueteComprimento, raqueteAltura )
}


function movimentoMinhaRaquete(){
  if (keyIsDown(UP_ARROW)) {
    yRaquete -= 10;
  }
   if (keyIsDown(DOWN_ARROW)) {
     yRaquete += 10;
   }
}

function verificaColisaoRaquete(){
if (xBolinha - raio < xRaquete + raqueteComprimento && yBolinha - raio < yRaquete + raqueteAltura && yBolinha + raio > yRaquete){
   velocidadeXBolinha *= -1;
  raquetada.play();
}
  }

function verificaColisaoRaquete(x,y){
 colidiu =
  collideRectCircle(x,y,raqueteComprimento,raqueteAltura,xBolinha,yBolinha,raio);
  if (colidiu){
    velocidadeXBolinha *= -1;
    raquetada.play();
  }
}

function movimentaRaqueteOponente(){
    if (keyIsDown(87)){
        yRaqueteOponente -= 10;
    }
    if (keyIsDown(83)){
        yRaqueteOponente += 10;
    }
}

function incluirPlacar(){
    stroke(255)
    textAlign(CENTER);
    textSize(16);
    fill(color(255,140, 0));
    rect(150, 10, 40, 20);
    fill(255);
    text(meusPontos, 170, 26);
    fill(color(255,140, 0));
    rect(450, 10, 40, 20);
    fill(255);
    text(pontosDoOponente, 470, 26);
}


function marcaPonto(){
  if (xBolinha > 590){
    meusPontos += 1;
    ponto.play();
  }
  if (xBolinha < 10){
    pontosDoOponente += 1;
    ponto.play();
  }
}
