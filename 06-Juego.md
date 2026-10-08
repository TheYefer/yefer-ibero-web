---
layout: default
title: Juego
nav_order: 6
---

## Mi Juego 3D en Canvas

Este es un motor de Raycasting estilo DOOM programado completamente en JavaScript, ejecutándose nativamente en la página.

<style>
  /* Limitamos los estilos solo al contenedor del juego para no romper tu portafolio */
  #game-wrapper {
    position: relative;
    width: 100%;
    max-width: 800px;
    height: 500px;
    margin: 20px auto;
    background-color: #333;
    border: 4px solid #222;
    border-radius: 8px;
    overflow: hidden;
    font-family: 'Courier New', Courier, monospace;
  }
  #gameCanvas {
    display: block;
    width: 100%;
    height: 100%;
    image-rendering: pixelated; /* Le da el toque retro */
  }
  #start-screen, #game-over-screen {
    position: absolute;
    top: 0; left: 0; width: 100%; height: 100%;
    background: rgba(0, 0, 0, 0.8);
    color: white;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    z-index: 10;
  }
  #game-over-screen { display: none; }
  #ui-layer {
    position: absolute;
    bottom: 10px; left: 10px;
    color: red;
    font-size: 24px;
    font-weight: bold;
    text-shadow: 2px 2px 0 #000;
    pointer-events: none;
    z-index: 5;
    display: none;
  }
  button {
    padding: 15px 30px;
    font-size: 24px;
    background: #8b0000;
    color: white;
    border: 2px solid #ff0000;
    cursor: pointer;
    font-family: 'Courier New', Courier, monospace;
    font-weight: bold;
    text-transform: uppercase;
  }
  button:hover { background: #ff0000; }
  .instructions { margin-top: 20px; font-size: 16px; text-align: center; color: #ccc;}
</style>

<div id="game-wrapper">
  <canvas id="gameCanvas" width="640" height="400"></canvas>
  
  <div id="ui-layer">
    HP: <span id="hp-display">100</span> | OLEADA: <span id="wave-display">1</span>
  </div>

  <div id="start-screen">
    <h1 style="color: red; font-size: 48px; margin: 0; text-shadow: 3px 3px 0 #000;">WEB DOOM</h1>
    <p class="instructions">
      <b>W, A, S, D</b>: Moverse<br>
      <b>Flechas Izq/Der</b>: Girar cámara<br>
      <b>Espacio</b>: Disparar / Abrir Puertas Amarillas
    </p>
    <button id="start-btn">Iniciar Juego</button>
  </div>

  <div id="game-over-screen">
    <h1 style="color: red; font-size: 48px; margin: 0;">HAS MUERTO</h1>
    <p style="font-size: 20px;">Llegaste a la oleada: <span id="final-wave">1</span></p>
    <button id="restart-btn" style="margin-top: 20px;">Reintentar</button>
  </div>
</div>

<script>
  // ==========================================
  // MOTOR DE RAYCASTING Y LÓGICA DEL JUEGO
  // ==========================================
  const canvas = document.getElementById('gameCanvas');
  const ctx = canvas.getContext('2d');
  const startBtn = document.getElementById('start-btn');
  const restartBtn = document.getElementById('restart-btn');
  const startScreen = document.getElementById('start-screen');
  const gameOverScreen = document.getElementById('game-over-screen');
  const uiLayer = document.getElementById('ui-layer');
  const hpDisplay = document.getElementById('hp-display');
  const waveDisplay = document.getElementById('wave-display');

  // Dimensiones internas
  const SCREEN_WIDTH = 640;
  const SCREEN_HEIGHT = 400;

  // Mapa del nivel (1 = Pared normal, 2 = Zona Roja, 3 = Puerta Amarilla, 0 = Vacío)
  let map = [
    [1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1],
    [1,0,0,0,0,0,1,2,2,2,2,2,2,2,2,0,0,0,1],
    [1,0,0,0,0,0,0,0,0,0,2,0,0,0,3,0,0,0,1],
    [1,0,0,0,0,0,1,2,0,0,0,0,0,0,2,0,0,0,1],
    [1,0,0,1,0,0,1,2,2,2,2,0,0,0,2,0,0,0,1],
    [1,0,0,1,0,0,1,1,1,1,1,0,0,0,0,1,1,1,1],
    [1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1],
    [1,1,1,1,1,1,1,1,1,1,1,1,1,1,1,1]
  ];
  const MAP_WIDTH = map[0].length;
  const MAP_HEIGHT = map.length;

  // Jugador
  let player = {
    x: 2.5, y: 2.5, 
    dirX: -1, dirY: 0, 
    planeX: 0, planeY: 0.66, 
    hp: 100
  };

  // Estado del juego
  let isPlaying = false;
  let wave = 1;
  let enemies = [];
  let keys = {};

  // Escuchar teclado
  window.addEventListener('keydown', (e) => { keys[e.code] = true; });
  window.addEventListener('keyup', (e) => { keys[e.code] = false; });

  // Controles de botones
  startBtn.addEventListener('click', startGame);
  restartBtn.addEventListener('click', startGame);

  function startGame() {
    startScreen.style.display = 'none';
    gameOverScreen.style.display = 'none';
    uiLayer.style.display = 'block';
    
    player.hp = 100;
    player.x = 2.5; player.y = 2.5;
    wave = 1;
    enemies = [];
    spawnEnemies();
    updateUI();
    isPlaying = true;
    gameLoop();
  }

  function spawnEnemies() {
    enemies = [];
    for(let i = 0; i < wave * 2; i++) {
      let ex, ey;
      do {
        ex = Math.floor(Math.random() * (MAP_WIDTH - 2)) + 1;
        ey = Math.floor(Math.random() * (MAP_HEIGHT - 2)) + 1;
      } while(map[ey][ex] !== 0 || (Math.abs(ex - player.x) < 2 && Math.abs(ey - player.y) < 2));
      
      enemies.push({ x: ex + 0.5, y: ey + 0.5, hp: 30, active: true });
    }
    waveDisplay.innerText = wave;
  }

  // Lógica de disparo e interacción con puertas
  window.addEventListener('keydown', (e) => {
    if(!isPlaying) return;
    if(e.code === 'Space') {
      // 1. Comprobar si hay una puerta enfrente
      let checkX = Math.floor(player.x + player.dirX);
      let checkY = Math.floor(player.y + player.dirY);
      if(map[checkY][checkX] === 3) {
        map[checkY][checkX] = 0; // Abre la puerta
        return;
      }

      // 2. Si no hay puerta, Disparar
      // Efecto visual rápido de disparo
      ctx.fillStyle = 'rgba(255, 255, 0, 0.5)';
      ctx.fillRect(0, 0, SCREEN_WIDTH, SCREEN_HEIGHT);
      
      // Comprobar colisión con enemigos
      enemies.forEach(enemy => {
        if(!enemy.active) return;
        let dx = enemy.x - player.x;
        let dy = enemy.y - player.y;
        let dist = Math.sqrt(dx*dx + dy*dy);
        // Ángulo hacia el enemigo
        let angleToEnemy = Math.atan2(dy, dx);
        let playerAngle = Math.atan2(player.dirY, player.dirX);
        
        let diff = Math.abs(angleToEnemy - playerAngle);
        if(diff > Math.PI) diff = 2 * Math.PI - diff;
        
        // Si el enemigo está en la mira (ángulo pequeño)
        if(diff < 0.2 && dist < 8) {
          enemy.active = false;
        }
      });

      // Pasar de oleada si matas a todos
      if(!enemies.some(e => e.active)) {
        wave++;
        spawnEnemies();
      }
    }
  });

  function update() {
    if(!isPlaying) return;
    
    const moveSpeed = 0.05;
    // Sensibilidad bajada como solicitaste
    const rotSpeed = 0.03; 

    // Rotación
    if (keys['ArrowRight'] || keys['KeyD']) {
      let oldDirX = player.dirX;
      player.dirX = player.dirX * Math.cos(-rotSpeed) - player.dirY * Math.sin(-rotSpeed);
      player.dirY = oldDirX * Math.sin(-rotSpeed) + player.dirY * Math.cos(-rotSpeed);
      let oldPlaneX = player.planeX;
      player.planeX = player.planeX * Math.cos(-rotSpeed) - player.planeY * Math.sin(-rotSpeed);
      player.planeY = oldPlaneX * Math.sin(-rotSpeed) + player.planeY * Math.cos(-rotSpeed);
    }
    if (keys['ArrowLeft'] || keys['KeyA']) {
      let oldDirX = player.dirX;
      player.dirX = player.dirX * Math.cos(rotSpeed) - player.dirY * Math.sin(rotSpeed);
      player.dirY = oldDirX * Math.sin(rotSpeed) + player.dirY * Math.cos(rotSpeed);
      let oldPlaneX = player.planeX;
      player.planeX = player.planeX * Math.cos(rotSpeed) - player.planeY * Math.sin(rotSpeed);
      player.planeY = oldPlaneX * Math.sin(rotSpeed) + player.planeY * Math.cos(rotSpeed);
    }

    // Movimiento
    if (keys['KeyW'] || keys['ArrowUp']) {
      if(map[Math.floor(player.y)][Math.floor(player.x + player.dirX * moveSpeed)] === 0) player.x += player.dirX * moveSpeed;
      if(map[Math.floor(player.y + player.dirY * moveSpeed)][Math.floor(player.x)] === 0) player.y += player.dirY * moveSpeed;
    }
    if (keys['KeyS'] || keys['ArrowDown']) {
      if(map[Math.floor(player.y)][Math.floor(player.x - player.dirX * moveSpeed)] === 0) player.x -= player.dirX * moveSpeed;
      if(map[Math.floor(player.y - player.dirY * moveSpeed)][Math.floor(player.x)] === 0) player.y -= player.dirY * moveSpeed;
    }

    // IA Enemigos
    enemies.forEach(enemy => {
      if(!enemy.active) return;
      let dx = player.x - enemy.x;
      let dy = player.y - enemy.y;
      let dist = Math.sqrt(dx*dx + dy*dy);
      
      if(dist > 0.5) {
        enemy.x += (dx/dist) * 0.01;
        enemy.y += (dy/dist) * 0.01;
      } else {
        // Atacar al jugador
        player.hp -= 0.5;
        updateUI();
        if(player.hp <= 0) {
          isPlaying = false;
          document.getElementById('final-wave').innerText = wave;
          gameOverScreen.style.display = 'flex';
          uiLayer.style.display = 'none';
        }
      }
    });
  }

  function updateUI() {
    hpDisplay.innerText = Math.max(0, Math.floor(player.hp));
  }

  function draw() {
    // Limpiar pantalla (Cielo y suelo)
    ctx.fillStyle = '#383838'; // Techo oscuro
    ctx.fillRect(0, 0, SCREEN_WIDTH, SCREEN_HEIGHT / 2);
    ctx.fillStyle = '#5c5c5c'; // Suelo gris
    ctx.fillRect(0, SCREEN_HEIGHT / 2, SCREEN_WIDTH, SCREEN_HEIGHT / 2);

    let zBuffer = new Array(SCREEN_WIDTH).fill(0);

    // Raycasting de Paredes
    for (let x = 0; x < SCREEN_WIDTH; x++) {
      let cameraX = 2 * x / SCREEN_WIDTH - 1;
      let rayDirX = player.dirX + player.planeX * cameraX;
      let rayDirY = player.dirY + player.planeY * cameraX;

      let mapX = Math.floor(player.x);
      let mapY = Math.floor(player.y);

      let sideDistX, sideDistY;
      let deltaDistX = Math.abs(1 / rayDirX);
      let deltaDistY = Math.abs(1 / rayDirY);
      let perpWallDist;

      let stepX, stepY;
      let hit = 0;
      let side = 0;

      if (rayDirX < 0) { stepX = -1; sideDistX = (player.x - mapX) * deltaDistX; } 
      else { stepX = 1; sideDistX = (mapX + 1.0 - player.x) * deltaDistX; }
      if (rayDirY < 0) { stepY = -1; sideDistY = (player.y - mapY) * deltaDistY; } 
      else { stepY = 1; sideDistY = (mapY + 1.0 - player.y) * deltaDistY; }

      // DDA
      while (hit === 0) {
        if (sideDistX < sideDistY) {
          sideDistX += deltaDistX;
          mapX += stepX;
          side = 0;
        } else {
          sideDistY += deltaDistY;
          mapY += stepY;
          side = 1;
        }
        if (map[mapY][mapX] > 0) hit = map[mapY][mapX];
      }

      if (side === 0) perpWallDist = (sideDistX - deltaDistX);
      else perpWallDist = (sideDistY - deltaDistY);

      zBuffer[x] = perpWallDist;

      let lineHeight = Math.floor(SCREEN_HEIGHT / perpWallDist);
      let drawStart = -lineHeight / 2 + SCREEN_HEIGHT / 2;
      if (drawStart < 0) drawStart = 0;
      let drawEnd = lineHeight / 2 + SCREEN_HEIGHT / 2;
      if (drawEnd >= SCREEN_HEIGHT) drawEnd = SCREEN_HEIGHT - 1;

      // Colores según tipo de pared
      let color;
      if(hit === 1) color = side === 1 ? '#0000aa' : '#0000ff'; // Pared Azul
      if(hit === 2) color = side === 1 ? '#aa0000' : '#ff0000'; // Zona Roja
      if(hit === 3) color = side === 1 ? '#aaaa00' : '#ffff00'; // Puerta Amarilla

      ctx.fillStyle = color;
      ctx.fillRect(x, drawStart, 1, drawEnd - drawStart);
    }

    // Dibujar Enemigos (Sprites básicos de raycasting)
    enemies.forEach(enemy => {
      if(!enemy.active) return;
      
      let spriteX = enemy.x - player.x;
      let spriteY = enemy.y - player.y;

      let invDet = 1.0 / (player.planeX * player.dirY - player.dirX * player.planeY);
      let transformX = invDet * (player.dirY * spriteX - player.dirX * spriteY);
      let transformY = invDet * (-player.planeY * spriteX + player.planeX * spriteY);

      let spriteScreenX = Math.floor((SCREEN_WIDTH / 2) * (1 + transformX / transformY));

      let spriteHeight = Math.abs(Math.floor(SCREEN_HEIGHT / transformY));
      let drawStartY = -spriteHeight / 2 + SCREEN_HEIGHT / 2;
      if (drawStartY < 0) drawStartY = 0;
      let drawEndY = spriteHeight / 2 + SCREEN_HEIGHT / 2;
      if (drawEndY >= SCREEN_HEIGHT) drawEndY = SCREEN_HEIGHT - 1;

      let spriteWidth = Math.abs(Math.floor(SCREEN_HEIGHT / transformY));
      let drawStartX = -spriteWidth / 2 + spriteScreenX;
      if (drawStartX < 0) drawStartX = 0;
      let drawEndX = spriteWidth / 2 + spriteScreenX;
      if (drawEndX >= SCREEN_WIDTH) drawEndX = SCREEN_WIDTH - 1;

      if(transformY > 0) {
        for(let stripe = drawStartX; stripe < drawEndX; stripe++) {
          if(transformY < zBuffer[stripe]) {
            // Dibujar bloque verde como enemigo
            ctx.fillStyle = '#00ff00';
            ctx.fillRect(stripe, drawStartY, 1, drawEndY - drawStartY);
          }
        }
      }
    });

    // Dibujar el "Arma" estática
    ctx.fillStyle = '#888';
    ctx.fillRect(SCREEN_WIDTH/2 - 20, SCREEN_HEIGHT - 100, 40, 100);
    ctx.fillStyle = '#444';
    ctx.fillRect(SCREEN_WIDTH/2 - 10, SCREEN_HEIGHT - 80, 20, 80);
  }

  function gameLoop() {
    if(!isPlaying) return;
    update();
    draw();
    requestAnimationFrame(gameLoop);
  }

  // Dibujar pantalla de fondo antes de iniciar
  draw();
</script>