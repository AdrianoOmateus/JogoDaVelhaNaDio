# JogoDaVelhaNaDio
Jogo da Velha utilizado WebStorm como IDE e na aplicação usada foi CSS, HTML e JAVASCRIPT

HTML ->


<!DOCTYPE html>
<html lang >:"pt-br"

<head>
    <title>
        Jogo da Velha
    </title>
    <meta charset="UTF-8">
    <link rel="stylesheet" href="estilo.css">
</head>

<body>
<h1>
    Jogo da Velha
</h1>
<div>
    <div id="1" class="quadrado" onclick="escolherQuadrado(this.id)">-</div>
    <div id="2" class="quadrado" onclick="escolherQuadrado(this.id)">-</div>
    <div id="3" class="quadrado" onclick="escolherQuadrado(this.id)">-</div>
</div>

<div>
    <div id="4" class="quadrado" onclick="escolherQuadrado(this.id)">-</div>
    <div id="5" class="quadrado" onclick="escolherQuadrado(this.id)">-</div>
    <div id="6" class="quadrado" onclick="escolherQuadrado(this.id)">-</div>
</div>

<div>
    <div id="7" class="quadrado" onclick="escolherQuadrado(this.id)">-</div>
    <div id="8" class="quadrado" onclick="escolherQuadrado(this.id)">-</div>
    <div id="9" class="quadrado" onclick="escolherQuadrado(this.id)">-</div>
</div>

<div class="jogador">
    <label>
        Jogador:
    </label>
    <label id="jogador-selecionado">

    </label>
</div>

<div class="vencedor">
    <label>
        Vencedor:
    </label>
    <label id="vencedor-selecionado">

    </label>
</div>

<div>
    <button onclick="reiniciar()">
        Reiniciar
    </button>
</div>
</body>

<script src="velha.js"></script>

</html>

CSS ->

body {
    text-align: center;
}
.quadrado {
    text-align: center;
    width: 58px;
    background: #eee;
    display: inline-block;
    padding: 48px;
    font-size: 68px;
    margin: 5px;
    cursor: pointer;
    color: #eee;
}
.jogador, .vencedor {
    font-size: 38px;
    margin-top: 18px;
}

button {
    margin-top: 18px;
    width: 188px;
    height: 38px;
    background: #eee;
    cursor: pointer;
}

JAVASCRIPT ->

var jogador, vencedor = null;
var jogadorSelecionado =  document.getElementById('jogador-selecionado');
var vencedorSelecionado = document.getElementById('vencedor-selecionado');
var quadrados = document.getElementsByClassName('quadrado');

mudarJogador('X');

function escolherQuadrado(id) {

   if (vencedor !== null) {
       return;
   }

  var quadrado = document.getElementById(id);
  if (quadrado.innerHTML !== '-') {
      return;
  }

    quadrado.innerHTML = jogador;
    quadrado.style.color = '#000';

  if (jogador === 'X') {
      jogador = 'O';
  }else {
      jogador = 'X';
  }

  mudarJogador(jogador);
  checaVencedor();
}

function mudarJogador(valor) {
    jogador = valor;
    jogadorSelecionado.innerHTML = jogador;

}
    
function checaVencedor(){
    var quadrado1 = document.getElementById(1);
    var quadrado2 = document.getElementById(2);
    var quadrado3 = document.getElementById(3);
    var quadrado4 = document.getElementById(4);
    var quadrado5 = document.getElementById(5);
    var quadrado6 = document.getElementById(6);
    var quadrado7 = document.getElementById(7);
    var quadrado8 = document.getElementById(8);
    var quadrado9 = document.getElementById(9);

    if (checaSequencia(quadrado1, quadrado2, quadrado3)) {
        mudaCorQuadrado(quadrado1, quadrado2,quadrado3);
        mudarVencedor(quadrado1);
        return
    }

    if (checaSequencia(quadrado4, quadrado5, quadrado6)) {
        mudaCorQuadrado(quadrado4, quadrado5,quadrado6);
        mudarVencedor(quadrado4);
        return;
    }

    if (checaSequencia(quadrado7, quadrado8, quadrado9)) {
        mudaCorQuadrado(quadrado7, quadrado8,quadrado9);
        mudarVencedor(quadrado7);
        return;
    }
    if (checaSequencia(quadrado1, quadrado4, quadrado7)) {
        mudaCorQuadrado(quadrado1, quadrado4, quadrado7);
        mudarVencedor(quadrado1);
        return;
    }
    if (checaSequencia(quadrado2, quadrado5, quadrado8)) {
        mudaCorQuadrado(quadrado2, quadrado5, quadrado8);
        mudarVencedor(quadrado2);
        return;
    }
    if (checaSequencia(quadrado3, quadrado6, quadrado9)) {
        mudaCorQuadrado(quadrado3, quadrado6, quadrado9);
        mudarVencedor(quadrado3);
        return;
    }
    if (checaSequencia(quadrado1, quadrado5, quadrado9)) {
        mudaCorQuadrado(quadrado1, quadrado5, quadrado9);
        mudarVencedor(quadrado1);
        return;
    }
    if (checaSequencia(quadrado3, quadrado5, quadrado7)) {
        mudaCorQuadrado(quadrado3, quadrado5,quadrado7);
        mudarVencedor(quadrado3);
    }
}


function mudarVencedor(quadrado) {
    vencedor = quadrado.innerHTML;
    vencedorSelecionado.innerHTML = vencedor;
}

function mudaCorQuadrado(quadrado1, quadrado2, quadrado3) {
    quadrado1.style.background = '#0f0';
    quadrado2.style.background = '#0f0';
    quadrado3.style.background = '#0f0';
}

function checaSequencia(quadrado1, quadrado2, quadrado3) {
    var eigual = false;

    if (quadrado1.innerHTML !== '-' && quadrado1.innerHTML === quadrado2.innerHTML && quadrado2.innerHTML === quadrado3.innerHTML) {
        eigual = true;
    }
    return eigual;
}
function reiniciar()
{
    vencedor = null;
    vencedorSelecionado.innerHTML = '';

    for (var i = 1; i <= 9; i++) {
        var quadrado = document.getElementById(i);
        quadrado.style.background = '#eee';
        quadrado.style.color = '#eee';
        quadrado.innerHTML = '-';
    }
    mudarJogador('X')
}
