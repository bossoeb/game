<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8" />
  <title>手機版貪吃蛇</title>
  <style>
    body { background:#111; display:flex; flex-direction:column; align-items:center; margin:0; }
    canvas { background:#222; margin-top:10px; }
    .controls { display:grid; grid-template-columns:80px 80px 80px; grid-gap:10px; margin-top:10px; }
    .controls button {
      width:80px; height:80px; font-size:24px; font-weight:bold;
      background:#333; color:#fff; border:none; border-radius:10px;
    }
  </style>
</head>
<body>
  <h2 style="color:white">🐍 手機版貪吃蛇</h2>
  <canvas id="game" width="400" height="400"></canvas>

  <div class="controls">
    <div></div><button onclick="setDir('UP')">↑</button><div></div>
    <button onclick="setDir('LEFT')">←</button><div></div><button onclick="setDir('RIGHT')">→</button>
    <div></div><button onclick="setDir('DOWN')">↓</button><div></div>
  </div>

  <script>
    const canvas = document.getElementById("game");
    const ctx = canvas.getContext("2d");
    const box = 20;
    let snake = [{x:9*box,y:10*box}];
    let food = {x:Math.floor(Math.random()*19)*box, y:Math.floor(Math.random()*19)*box};
    let dir;
    let score=0;

    document.addEventListener("keydown", e=>{
      if(e.key==="ArrowLeft" && dir!=="RIGHT") dir="LEFT";
      if(e.key==="ArrowUp" && dir!=="DOWN") dir="UP";
      if(e.key==="ArrowRight" && dir!=="LEFT") dir="RIGHT";
      if(e.key==="ArrowDown" && dir!=="UP") dir="DOWN";
    });

    function setDir(d){ if((d==="LEFT"&&dir!=="RIGHT")||(d==="RIGHT"&&dir!=="LEFT")||(d==="UP"&&dir!=="DOWN")||(d==="DOWN"&&dir!=="UP")) dir=d; }

    // 手機滑動控制
    let touchStartX=0, touchStartY=0;
    canvas.addEventListener("touchstart", e=>{
      touchStartX=e.touches[0].clientX;
      touchStartY=e.touches[0].clientY;
    });
    canvas.addEventListener("touchend", e=>{
      let dx=e.changedTouches[0].clientX-touchStartX;
      let dy=e.changedTouches[0].clientY-touchStartY;
      if(Math.abs(dx)>Math.abs(dy)) setDir(dx>0?"RIGHT":"LEFT");
      else setDir(dy>0?"DOWN":"UP");
    });

    function draw(){
      ctx.fillStyle="#222"; ctx.fillRect(0,0,400,400);
      for(let i=0;i<snake.length;i++){
        ctx.fillStyle=i===0?"#0f0":"#0a0";
        ctx.fillRect(snake[i].x,snake[i].y,box,box);
      }
      ctx.fillStyle="#f00"; ctx.fillRect(food.x,food.y,box,box);
      let headX=snake[0].x, headY=snake[0].y;
      if(dir==="LEFT") headX-=box;
      if(dir==="UP") headY-=box;
      if(dir==="RIGHT") headX+=box;
      if(dir==="DOWN") headY+=box;
      if(headX===food.x && headY===food.y){
        score++;
        food={x:Math.floor(Math.random()*19)*box, y:Math.floor(Math.random()*19)*box};
      }else{ snake.pop(); }
      let newHead={x:headX,y:headY};
      if(headX<0||headY<0||headX>=400||headY>=400||snake.some(p=>p.x===newHead.x&&p.y===newHead.y)){
        clearInterval(game); alert("遊戲結束！分數："+score);
      }
      snake.unshift(newHead);
      ctx.fillStyle="#fff"; ctx.font="16px Arial"; ctx.fillText("分數:"+score,10,20);
    }
    let game=setInterval(draw,150);
  </script>
</body>
</html
