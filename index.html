<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>UFO - Arena Combat (Web)</title>
<style>
    body { margin: 0; overflow: hidden; background: #14142f; }
    canvas { display: block; margin: 0 auto; background: #14142f; }
</style>
</head>
<body>
<canvas id="gameCanvas" width="800" height="600"></canvas>
<script>
const canvas = document.getElementById('gameCanvas');
const ctx = canvas.getContext('2d');

const SCREEN_WIDTH = canvas.width;
const SCREEN_HEIGHT = canvas.height;

let keys = {};
let mouse = {x: 0, y: 0, down: false};
let FPS = 60;
let gameOver = false;
let paused = false;
let score = 0;
let combo = 0;
let comboTimer = 0;
let startTime = Date.now();
let enemySpawnCounter = 0;
let difficulty = 0;

class Player {
    constructor(x, y) {
        this.x = x;
        this.y = y;
        this.radius = 20;
        this.boost = false;
        this.bullets = [];
        this.lastShot = 0;
        this.rapidFire = false;
        this.rapidFireEndTime = 0;
    }
}
let player = new Player(SCREEN_WIDTH/2, SCREEN_HEIGHT/2);

let enemies = [];
let powerups = [];

// Powerup classes
class Powerup {
    constructor(x, y) { this.x = x; this.y = y; this.radius = 10; }
    update() { return true; }
    getColor() { return 'yellow'; }
    apply(player) {}
}

class RapidFirePowerup extends Powerup {
    getColor() { return 'orange'; }
    apply(player) {
        player.rapidFire = true;
        player.rapidFireEndTime = Date.now() + 5000;
    }
}
class ScorePowerup extends Powerup {
    getColor() { return 'lime'; }
    apply(player) { score += 50; }
}

// Input events
document.addEventListener('keydown', e => {
    keys[e.key.toLowerCase()] = true;
    if(e.key.toLowerCase() === 'c') paused = !paused;
    if(e.key.toLowerCase() === 'r' && gameOver) restartGame();
    if(e.key === ' ') player.boost = true;
});
document.addEventListener('keyup', e => {
    keys[e.key.toLowerCase()] = false;
    if(e.key === ' ') player.boost = false;
});
canvas.addEventListener('mousemove', e => {
    mouse.x = e.offsetX;
    mouse.y = e.offsetY;
});
canvas.addEventListener('mousedown', e => mouse.down = true);
canvas.addEventListener('mouseup', e => mouse.down = false);

// Game functions
function spawnEnemy() {
    const side = ['top','bottom','left','right'][Math.floor(Math.random()*4)];
    let x, y;
    if(side==='top'){x=Math.random()*SCREEN_WIDTH;y=-30;}
    else if(side==='bottom'){x=Math.random()*SCREEN_WIDTH;y=SCREEN_HEIGHT+30;}
    else if(side==='left'){x=-30;y=Math.random()*SCREEN_HEIGHT;}
    else{x=SCREEN_WIDTH+30;y=Math.random()*SCREEN_HEIGHT;}
    enemies.push({x, y, speed:1.5 + difficulty*0.2, health:1, radius:12});
}

function spawnPowerup(x,y){
    if(Math.random()<0.5) powerups.push(new RapidFirePowerup(x,y));
    else powerups.push(new ScorePowerup(x,y));
}

function createBullet(x,y){
    let dx = mouse.x - x;
    let dy = mouse.y - y;
    let dist = Math.sqrt(dx*dx + dy*dy);
    let speed = 8;
    let vx = dist>0 ? dx/dist*speed : 0;
    let vy = dist>0 ? dy/dist*speed : -speed;
    player.bullets.push({x,y,vx,vy,radius:4});
}

function updateEnemies(){
    for(let i=enemies.length-1;i>=0;i--){
        let e=enemies[i];
        let dx=player.x-e.x;
        let dy=player.y-e.y;
        let dist=Math.sqrt(dx*dx+dy*dy);
        if(dist>1){ e.x+=dx/dist*e.speed; e.y+=dy/dist*e.speed;}
        // Bullet collision
        for(let j=player.bullets.length-1;j>=0;j--){
            let b=player.bullets[j];
            let bd=Math.sqrt((b.x-e.x)**2 + (b.y-e.y)**2);
            if(bd<25){
                e.health-=1;
                player.bullets.splice(j,1);
                if(e.health<=0){
                    enemies.splice(i,1);
                    combo++; comboTimer=120;
                    score += 10+combo*5;
                    if(Math.random()<0.3) spawnPowerup(e.x,e.y);
                }
                break;
            }
        }
        // Player collision
        if(Math.sqrt((player.x-e.x)**2 + (player.y-e.y)**2)<40){
            gameOver = true;
        }
    }
}

function updatePowerups(){
    for(let i=powerups.length-1;i>=0;i--){
        let p=powerups[i];
        let dist=Math.sqrt((player.x-p.x)**2 + (player.y-p.y)**2);
        if(dist<35){
            p.apply(player);
            powerups.splice(i,1);
        }
    }
}

function restartGame(){
    gameOver = false;
    enemies=[]; powerups=[]; score=0; combo=0; startTime=Date.now();
    player.x=SCREEN_WIDTH/2; player.y=SCREEN_HEIGHT/2; player.bullets=[]; player.rapidFire=false;
    difficulty=0; enemySpawnCounter=0;
}

// Game loop
function gameLoop(){
    requestAnimationFrame(gameLoop);
    if(paused) return;
    // Clear
    ctx.fillStyle='#14142f';
    ctx.fillRect(0,0,SCREEN_WIDTH,SCREEN_HEIGHT);
    // Draw grid
    ctx.strokeStyle='rgba(40,40,70,0.5)';
    for(let x=0;x<SCREEN_WIDTH;x+=50){ctx.beginPath();ctx.moveTo(x,0);ctx.lineTo(x,SCREEN_HEIGHT);ctx.stroke();}
    for(let y=0;y<SCREEN_HEIGHT;y+=50){ctx.beginPath();ctx.moveTo(0,y);ctx.lineTo(SCREEN_WIDTH,y);ctx.stroke();}
    // Player movement
    let dx=0,dy=0;
    if(keys['a']) dx=-4;
    if(keys['d']) dx=4;
    if(keys['w']) dy=-4;
    if(keys['s']) dy=4;
    if(player.boost){dx*=1.5;dy*=1.5;}
    player.x = Math.max(10, Math.min(SCREEN_WIDTH-10, player.x+dx));
    player.y = Math.max(10, Math.min(SCREEN_HEIGHT-10, player.y+dy));
    // Fire bullets
    let now = Date.now();
    let fireCooldown = player.rapidFire ? 20 : 50;
    if(mouse.down && now - player.lastShot > fireCooldown){createBullet(player.x,player.y); player.lastShot=now;}
    // Update bullets
    for(let i=player.bullets.length-1;i>=0;i--){
        let b=player.bullets[i];
        b.x+=b.vx; b.y+=b.vy;
        if(b.x<-10 || b.x>SCREEN_WIDTH+10 || b.y<-10 || b.y>SCREEN_HEIGHT+10) player.bullets.splice(i,1);
    }
    updateEnemies();
    updatePowerups();
    // Combo timer
    if(comboTimer>0) comboTimer--; else combo=0;
    // Spawn enemies
    enemySpawnCounter++;
    let spawnRate=Math.max(20,100-Math.floor(difficulty*8));
    if(enemySpawnCounter>spawnRate){enemySpawnCounter=0;spawnEnemy();}
    // Increase difficulty
    difficulty=(Date.now()-startTime)/15000;
    // Rapid fire expire
    if(player.rapidFire && Date.now()>player.rapidFireEndTime) player.rapidFire=false;
    // Draw powerups
    for(let p of powerups){ctx.fillStyle=p.getColor();ctx.beginPath();ctx.arc(p.x,p.y,p.radius,0,Math.PI*2);ctx.fill();ctx.strokeStyle='white';ctx.stroke();}
    // Draw bullets
    ctx.fillStyle='lime';
    for(let b of player.bullets){ctx.beginPath();ctx.arc(b.x,b.y,b.radius,0,Math.PI*2);ctx.fill();}
    // Draw enemies
    ctx.fillStyle='red';
    for(let e of enemies){ctx.beginPath();ctx.arc(e.x,e.y,e.radius,0,Math.PI*2);ctx.fill();}
    // Draw player
    ctx.fillStyle='cyan';
    ctx.beginPath(); ctx.arc(player.x,player.y,player.radius,0,Math.PI*2); ctx.fill();
    ctx.strokeStyle='aqua'; ctx.stroke();
    // HUD
    ctx.fillStyle='white'; ctx.font='20px Arial';
    let elapsedS = Math.floor((Date.now()-startTime)/1000);
    ctx.fillText(`Time: ${elapsedS}s`,10,30);
    ctx.fillText(`Score: ${score}`,10,60);
    ctx.fillStyle='red'; ctx.fillText(`Enemies: ${enemies.length}`,10,90);
    if(combo>0){ctx.fillStyle=comboTimer>60?'yellow':'orange';ctx.fillText(`AHHH... x${combo}!`,SCREEN_WIDTH-250,30);}
    if(player.rapidFire){ctx.fillStyle='orange';ctx.fillText(`Rapid Fire: ${((player.rapidFireEndTime-Date.now())/1000).toFixed(1)}s`,10,120);}
    // Game over
    if(gameOver){
        ctx.fillStyle='rgba(0,0,0,0.7)'; ctx.fillRect(0,0,SCREEN_WIDTH,SCREEN_HEIGHT);
        ctx.fillStyle='red'; ctx.font='40px Arial'; ctx.fillText("YOU DIED!",SCREEN_WIDTH/2-100,SCREEN_HEIGHT/2-60);
        ctx.fillStyle='white'; ctx.font='30px Arial';
        ctx.fillText(`Final Score: ${score}`,SCREEN_WIDTH/2-100,SCREEN_HEIGHT/2);
        ctx.fillText(`Survived: ${elapsedS}s`,SCREEN_WIDTH/2-100,SCREEN_HEIGHT/2+40);
        ctx.font='20px Arial'; ctx.fillText(`(Press R to restart)`,SCREEN_WIDTH/2-80,SCREEN_HEIGHT/2+80);
    }
}
gameLoop();
</script>
</body>
</html>
