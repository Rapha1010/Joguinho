# Joguinho de Nave
Usando canvas JS para fazer movimentos, colisões e pontuação.


<!DOCTYPE html>
<html>
		<head>
			<title>Primeiro</title>

		<style type="text/css">
			canvas{

				border:1px solid #000;
				background:black;

			}
			</style>
		</head>


<body onload="inicializar()">
<canvas id="canvas" width="900" height="500">
Navegador não suporta
</canvas>	
<script type="text/javascript">

var naveAltura, naveLargura, navePosicaoX, velocidade, laserDiametro,laserposicaoX,laserposicaoY,danosJogador,colisao, pause,time;

function inicializar(){


pause=false;
naveAltura = 15;
naveLargura = 200;
danosJogador = 0;
time=0;



navePosicaoX = (canvas.width - naveLargura)/2;
velocidade =20;

canvas = document.getElementById("canvas");
context = canvas.getContext("2d");

laserDiametro = 10;
laserposicaoX = Math.random() * 900;
laserposicaoY = 0;


document.addEventListener('keydown', keyDown);

setInterval(gLoop, 30);
				
			
}
function keyDown(e) 
	{
    if(e.keyCode == 37 ){  

if (navePosicaoX > 0){
    
        navePosicaoX -= velocidade;

    }
	}
    if(e.keyCode == 39)
    {	

    	if (navePosicaoX < canvas.width - naveLargura + 25){

        navePosicaoX += velocidade;
	}


}

}
  

function gLoop(){

if(!pause){

context.clearRect(0,0,canvas.width,canvas.height);


// Criação da X-wing

context.fillStyle = 'gray';

context.fillRect(navePosicaoX + 68, canvas.height - naveAltura - 70, naveLargura - 150, naveAltura);

context.fillStyle = 'red';

context.fillRect(navePosicaoX + 68, canvas.height - naveAltura - 50, naveLargura - 150, naveAltura);

context.fillStyle = 'gray';

context.fillRect(navePosicaoX + 68, canvas.height - naveAltura - 30, naveLargura - 150, naveAltura);

context.fillStyle = 'red';

context.fillRect(navePosicaoX + 45, canvas.height - naveAltura - 10, naveLargura - 100, naveAltura);

context.fillStyle = 'gray';

context.fillRect(navePosicaoX + 20, canvas.height - naveAltura     , naveLargura - 50, naveAltura);

context.beginPath();

context.fillStyle = 'red';

context.arc(laserposicaoX, laserposicaoY, laserDiametro, 0, Math.PI * 2, true);

context.fill();


//Gravidade



if( laserposicaoY > (canvas.height) ){

	laserposicaoY =  0;

	laserposicaoX = Math.random() * 900;

	colisao = false;

	
}


if(laserposicaoY <=(canvas.height)){

laserposicaoY+=velocidade;

time+=1;


}

//Colisao

if((laserposicaoX > navePosicaoX && (laserposicaoX < navePosicaoX + naveLargura)) && laserposicaoY >= canvas.height && colisao == false){


danosJogador++;

colisao = true;

} 

if (danosJogador == 5){

context.fillText("Game Over",450,250);

danosJogador=0;

pause=true;

}

}

context.font = "20pt Calibri";

context.fillStyle = 'red';

context.fillText("Danos X-Wing: "+danosJogador, canvas.width - 850, 50);

context.fillStyle = 'blue';

context.fillText("       Tempo: "+time, canvas.width - 850, 80);

}


</script>

</body>
</html>
