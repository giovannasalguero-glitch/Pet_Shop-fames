<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <meta name="description" content="Pet Station: una misión pixel art de rescate y adopción responsable.">
  <title>Pet Station: Misión Rescate</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <main class="site-shell">
    <section class="game-card" aria-labelledby="game-title">
      <div class="title-block">
        <div>
          <p class="eyebrow">PET STATION · CUIDADO QUE TRANSFORMA VIDAS</p>
          <h1 id="game-title">PET STATION: MISIÓN RESCATE</h1>
        </div>
        <div class="status-chip"><span></span> RESCATE ACTIVO</div>
      </div>

      <div class="game-layout">
        <section class="stage-wrap" aria-label="Área principal del juego">
          <div class="hud" aria-live="polite">
            <div class="hud-cell hearts-cell">
              <span class="hud-label">VIDA</span>
              <span id="hearts" class="hearts" aria-label="5 de 5 corazones"><span>♥</span> <span>♥</span> <span>♥</span> <span>♥</span> <span>♥</span></span>
            </div>
            <div class="hud-cell">
              <span class="hud-label">NIVEL</span>
              <strong id="level-display">01 / 03</strong>
            </div>
            <div class="hud-cell">
              <span class="hud-label">PUNTOS</span>
              <strong id="score-display">000000</strong>
            </div>
            <div class="hud-cell enemies-cell">
              <span class="hud-label">RETOS</span>
              <strong id="enemy-display">03</strong>
            </div>
          </div>

          <div class="canvas-shell">
            <canvas
              id="game-canvas"
              width="960"
              height="540"
              tabindex="0"
              data-game-state="menu"
              data-player-x="480"
              data-player-y="440"
              data-tears="0"
              aria-label="Juego Pet Station. Usa WASD para moverte y las flechas para ayudar en la misión."
            ></canvas>
            <div id="screen-vignette" aria-hidden="true"></div>

            <section id="menu-screen" class="overlay overlay-main">
              <div class="sigil pet-sigil" aria-hidden="true"><span>♥</span></div>
              <div class="menu-pixels" aria-hidden="true"><span class="paw paw-one">●</span><span class="paw paw-two">●</span><span class="bone">━</span><span class="ball">●</span><span class="menu-heart">♥</span></div>
              <p class="overlay-kicker">CADA HUELLA CUENTA</p>
              <h2>Una misión para dar amor.</h2>
              <p class="overlay-copy">Rescata, protege y acompaña a cada mascota hasta encontrar un hogar lleno de cariño.</p>
              <div class="overlay-actions">
                <button id="play-button" class="button button-primary">PLAY</button>
                <button id="instructions-button" class="button button-ghost">INSTRUCCIONES</button>
              </div>
            </section>

            <section id="instructions-screen" class="overlay hidden" role="dialog" aria-modal="true" aria-labelledby="instructions-title">
              <p class="overlay-kicker">GUÍA DE RESCATE</p>
              <h2 id="instructions-title">Muévete y ayuda.</h2>
              <div class="instructions-grid">
                <div><kbd>W</kbd><kbd>A</kbd><kbd>S</kbd><kbd>D</kbd><strong>MOVERSE</strong><span>Camina en ocho direcciones.</span></div>
                <div><kbd>↑</kbd><kbd>←</kbd><kbd>↓</kbd><kbd>→</kbd><strong>AYUDAR</strong><span>Envía ayuda en cuatro direcciones.</span></div>
              </div>
              <p class="warning-copy">Las rocas bloquean el paso. Completa cada sala para abrir la puerta y liberar a una mascota. Pulsa P o Esc para pausar.</p>
              <button id="close-instructions" class="button button-primary">ENTENDIDO</button>
            </section>

            <section id="pause-screen" class="overlay hidden">
              <p class="overlay-kicker">TOMA UN RESPIRO</p>
              <h2>PAUSA</h2>
              <div class="overlay-actions">
                <button id="resume-button" class="button button-primary">CONTINUAR</button>
                <button id="pause-restart-button" class="button button-ghost">REINICIAR PARTIDA</button>
              </div>
            </section>

            <section id="transition-screen" class="overlay transition-overlay hidden" aria-live="assertive">
              <p id="transition-kicker" class="overlay-kicker">NIVEL SUPERADO</p>
              <h2 id="transition-title">LAS CATACUMBAS</h2>
              <p id="transition-copy" class="overlay-copy">Cada rescate abre una nueva oportunidad.</p>
            </section>

            <section id="end-screen" class="overlay hidden" aria-live="assertive">
              <p id="end-kicker" class="overlay-kicker">VOLVAMOS A INTENTARLO</p>
              <h2 id="end-title">MISIÓN PAUSADA</h2>
              <p id="end-copy" class="overlay-copy">Cada intento ayuda a construir un futuro mejor.</p>
              <div class="final-score">PUNTUACIÓN <strong id="final-score">000000</strong></div>
              <button id="end-restart-button" class="button button-primary">VOLVER A INTENTAR</button>
            </section>
          </div>

          <div class="game-toolbar">
            <button id="pause-button" class="tool-button" aria-label="Pausar juego">Ⅱ <span>PAUSA</span></button>
            <button id="restart-button" class="tool-button" aria-label="Reiniciar juego">↻ <span>REINICIAR</span></button>
            <button id="mute-button" class="tool-button" aria-label="Silenciar sonido" aria-pressed="false">◖)) <span>SONIDO</span></button>
            <p class="room-name"><span id="room-dot"></span> <strong id="room-name">REFUGIO CANINO</strong></p>
          </div>
        </section>

        <aside class="mission-panel" aria-label="Información de la misión">
          <div class="mission-number">03</div>
          <p class="panel-kicker">RUTA DE RESCATE</p>
          <ol class="level-list">
            <li class="active" data-level="1"><span>01</span><div><strong>REFUGIO CANINO</strong><small>Un perrito espera su segunda oportunidad.</small></div></li>
            <li data-level="2"><span>02</span><div><strong>REFUGIO FELINO</strong><small>Un gatito espera una familia.</small></div></li>
            <li data-level="3"><span>03</span><div><strong>REFUGIO ALADO</strong><small>Un pajarito sueña con volver a cantar.</small></div></li>
          </ol>

          <div class="controls-card">
            <p class="panel-kicker">CONTROLES</p>
            <div><span class="key-row"><kbd>W</kbd><kbd>A</kbd><kbd>S</kbd><kbd>D</kbd></span><strong>MOVIMIENTO</strong></div>
            <div><span class="key-row"><kbd>↑</kbd><kbd>←</kbd><kbd>↓</kbd><kbd>→</kbd></span><strong>AYUDA</strong></div>
          </div>

          <blockquote>“Adoptar transforma dos vidas: la suya y la tuya.”</blockquote>
          <div class="objective">
            <span>OBJETIVO ACTUAL</span>
            <strong id="objective-text">ABRE CAMINO PARA EL RESCATE</strong>
            <a class="promo-banner" href="https://www.petstation.ec/?sc=1" target="_blank" rel="noopener noreferrer" aria-label="Visitar Pet Station">
              <img src="assets/images/pet-station-promo.png" alt="Pet Station: regístrate y recibe recompensas">
            </a>
          </div>
        </aside>
      </div>
    </section>
    <footer><span>© PET STATION</span><span>ADOPTAR ES UN ACTO DE AMOR</span></footer>
  </main>
  <script src="game.js"></script>
</body>
</html>
