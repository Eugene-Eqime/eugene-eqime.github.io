<body style="text-align: center;">
<canvas id='c' width='320' height='455'></canvas>
</body>
<style>
    *{margin: 0;padding: 0;}
    html, body{
        height: 100%;
        align-items: center;
        justify-content: center;
        display: flex;
        background-color: #242424;
    }
</style>
<script>
var cnv = document.getElementById('c');
var ctx = cnv.getContext('2d');
var tr = {
x: 420,
y: 20,
size: 100,
}
var player = {
size: 50,
x: 220/2,
y: 235/2,
speed: 5,
}
var score = 0;
function clear(){
ctx.fillStyle = 'rgb(102, 227, 190)';
ctx.fillRect(0,0,window.innerWidth, window.innerHeight);
}
function an(){
player.speed=9; 
player.speed*=-1;
}
cnv.onclick = function(){
an();
}
window.onkeypress = function(event){
    if(event.which == 32){
        an();
    }
}
function random(min, max){
var rand = Math.floor(min + Math.random()*(max + 1 - min));
return rand;
}
function dead() {
    tr.x = 1000;
    score = 0;
    player.y = 235 / 2;
}
function game() {
	clear();
    player.y += player.speed;
    player.speed += 0.4;
    tr.x -= 4;
    ctx.fillStyle = 'rgb(36, 187, 63)';
    ctx.fillRect(tr.x, 0, tr.size, 455);
    ctx.fillStyle = 'rgb(102, 227, 190)';
    ctx.fillRect(tr.x, tr.y, tr.size, tr.size * 2)
    ctx.fillStyle = 'rgb(247, 193, 53)';
    ctx.fillRect(player.x - player.size / 2, player.y - player.size / 2, player.size, player.size);
    ctx.font = '60px Arial';
    ctx.fillStyle = 'white';
    ctx.fillText(score, cnv.width/2-15, cnv.height / 5);
    if (tr.x + 100 < 0) {
        tr.x = 320;
        tr.y = random(20, 240);
        score++;
    }
    if (tr.x <= player.x + player.size/2 && player.y - player.size / 2 < tr.y || tr.x <= player.x - player.size/2 + player.size/2 && player.y + player.size / 2 > tr.y + 200) {
        dead();
    }
}
function jump() {
    if (player.y + player.size/2+20 > tr.y + 200) {
       an();
    }
    ctx.font = '15px Arial';
    ctx.fillStyle = 'red';
    ctx.fillText('(Y1: ' + tr.y + ' X1: ' + tr.x + ')', tr.x - 10, tr.y + 15);
    ctx.fillText('(Y2: ' + tr.y + '+200' + ' X2: ' + tr.x + ')', tr.x - 10, tr.y+200 - 10);
    ctx.fillStyle = 'red';
    ctx.fillRect(player.x-3, player.y-3, 6, 6);
    ctx.fillRect(tr.x - 3, tr.y - 3, 6, 6);
    ctx.fillRect(tr.x - 3, tr.y + 200 - 3, 6, 6);
    ctx.strokeStyle = 'red';
    ctx.beginPath();
    ctx.moveTo(player.x, player.y);
    ctx.lineTo(tr.x, tr.y);
    ctx.stroke()
    ctx.beginPath();
    ctx.moveTo(player.x, player.y);
    ctx.lineTo(tr.x, tr.y+200);
    ctx.stroke();
}
setInterval(game, 1000/60);
//setInterval(jump, 1000/60);
</script>
