<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Manuel Otaiza — Presentación</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Oswald:wght@400;600;700&family=IBM+Plex+Sans:wght@400;500;600&family=IBM+Plex+Mono:wght@500&display=swap" rel="stylesheet">
<style>
  :root{
    --noche:#0A1F2B;
    --noche-2:#0E2B39;
    --cal:#F2F0E9;
    --grana:#8E1B3F;
    --azul:#1348A0;
    --pasto:#2E7D5B;
    --arena:#D8C7A1;
 
    --display:"Oswald","Haettenschweiler","Arial Narrow",Impact,sans-serif;
    --texto:"IBM Plex Sans",system-ui,-apple-system,Segoe UI,sans-serif;
    --dato:"IBM Plex Mono",ui-monospace,Menlo,Consolas,monospace;
  }
 
  *{box-sizing:border-box}
  html{scroll-behavior:smooth}
  body{
    margin:0;
    background:var(--noche);
    color:var(--cal);
    font-family:var(--texto);
    line-height:1.6;
    -webkit-font-smoothing:antialiased;
  }
  .envoltura{max-width:1060px;margin:0 auto;padding:0 24px}
 
  /* ---------- Navegación ---------- */
  .menu{
    position:sticky;top:0;z-index:20;
    background:rgba(10,31,43,.92);
    backdrop-filter:blur(8px);
    border-bottom:1px solid rgba(242,240,233,.16);
  }
  .menu ul{
    display:flex;flex-wrap:wrap;gap:24px;
    list-style:none;margin:0;padding:14px 24px;
    max-width:1060px;margin:0 auto;
  }
  .menu a{
    color:rgba(242,240,233,.72);
    text-decoration:none;
    font-family:var(--dato);
    font-size:11px;
    letter-spacing:.18em;
    text-transform:uppercase;
  }
  .menu a:hover,.menu a:focus-visible{color:var(--arena)}
 
  /* ---------- Portada ---------- */
  .portada{
    position:relative;
    overflow:hidden;
    padding:72px 0 56px;
    border-bottom:1px solid rgba(242,240,233,.16);
    background:radial-gradient(120% 80% at 50% 0%, var(--noche-2) 0%, var(--noche) 62%);
  }
  .lineas{position:absolute;inset:0;opacity:.14;pointer-events:none}
  .rotulo{
    font-family:var(--dato);
    font-size:12px;letter-spacing:.22em;text-transform:uppercase;
    color:var(--arena);margin:0 0 14px;position:relative;
  }
  .nombre{
    position:relative;
    font-family:var(--display);font-weight:700;text-transform:uppercase;
    font-size:clamp(52px,13vw,142px);line-height:.86;letter-spacing:-.01em;margin:0;
  }
  .nombre span{display:block}
  .nombre .apellido{color:var(--arena)}
  .bajada{
    position:relative;max-width:52ch;margin:24px 0 0;
    font-size:clamp(16px,2.2vw,19px);color:rgba(242,240,233,.85);
  }
  .porque{
    position:relative;
    margin-top:40px;
    max-width:60ch;
    border-left:3px solid var(--grana);
    padding-left:22px;
  }
  .porque h2{
    font-family:var(--display);font-weight:600;text-transform:uppercase;
    font-size:clamp(20px,3.4vw,28px);line-height:1.1;letter-spacing:.01em;
    margin:0 0 10px;color:var(--arena);
  }
  .porque p{margin:0;color:rgba(242,240,233,.85);font-size:16px}
  .porque a{color:var(--cal);text-underline-offset:4px;text-decoration-thickness:1px}
  .porque a:hover{color:var(--arena)}
 
  .datos{
    position:relative;display:flex;flex-wrap:wrap;margin-top:36px;
    border-top:1px solid rgba(242,240,233,.18);
  }
  .dato{flex:1 1 180px;padding:16px 20px 16px 0;border-right:1px solid rgba(242,240,233,.12)}
  .dato:last-child{border-right:0}
  .dato dt{
    font-family:var(--dato);font-size:11px;letter-spacing:.18em;
    text-transform:uppercase;color:rgba(242,240,233,.55);margin:0 0 4px;
  }
  .dato dd{
    margin:0;font-family:var(--display);font-weight:600;font-size:20px;
    letter-spacing:.02em;text-transform:uppercase;
  }
 
  /* ---------- Secciones ---------- */
  section{padding:76px 0;border-bottom:1px solid rgba(242,240,233,.12)}
  .titulo{
    font-family:var(--display);font-weight:600;text-transform:uppercase;
    font-size:clamp(30px,5.4vw,50px);letter-spacing:.01em;line-height:1;margin:0 0 10px;
  }
  .subtitulo{margin:0 0 40px;color:rgba(242,240,233,.7);max-width:54ch}
 
  /* ---------- Hobbies (tarjetas) ---------- */
  .tarjetas{display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:20px}
  .tarjeta{
    border:1px solid rgba(242,240,233,.22);
    background:var(--noche-2);
    padding:26px 24px 28px;
    display:flex;flex-direction:column;gap:10px;
    border-top:3px solid var(--arena);
    transition:transform .2s ease,border-color .2s ease,background .2s ease;
    animation:entrar .5s ease backwards;
  }
  .tarjeta:hover{transform:translateY(-4px);background:#123244;border-top-color:var(--grana)}
  .tarjeta .etiqueta{
    font-family:var(--dato);font-size:11px;letter-spacing:.2em;
    text-transform:uppercase;color:var(--arena);margin:0;
  }
  .tarjeta h3{
    font-family:var(--display);font-weight:600;text-transform:uppercase;
    font-size:clamp(22px,3.2vw,28px);line-height:1.05;margin:0;
  }
  .tarjeta p{margin:0;font-size:15px;color:rgba(242,240,233,.82)}
  @keyframes entrar{from{opacity:0;transform:translateY(14px)}}
 
  /* ---------- Series ---------- */
  .series{display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:20px}
  .serie{
    border:1px solid rgba(242,240,233,.22);
    padding:26px 22px;background:var(--noche-2);
    display:flex;flex-direction:column;gap:10px;
  }
  .serie .puesto-lista{
    font-family:var(--dato);font-size:11px;letter-spacing:.2em;
    color:var(--arena);text-transform:uppercase;
  }
  .serie h3{
    font-family:var(--display);font-weight:600;text-transform:uppercase;
    font-size:clamp(20px,3vw,26px);line-height:1.05;margin:0;
  }
  .serie p{margin:0;font-size:15px;color:rgba(242,240,233,.8)}
 
  /* ---------- Fútbol ---------- */
  .equipos{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:24px;margin-top:32px}
  .equipo{
    position:relative;overflow:hidden;
    border:1px solid rgba(242,240,233,.22);
    padding:28px;min-height:220px;
    display:flex;flex-direction:column;justify-content:flex-end;
  }
  .equipo .franjas{position:absolute;inset:0;opacity:.9}
  .equipo--blaugrana .franjas{background:repeating-linear-gradient(90deg,var(--grana) 0 14%, var(--azul) 14% 28%)}
  .equipo--azul .franjas{background:linear-gradient(160deg,var(--azul) 0%, #0A2E6B 100%)}
  .equipo .velo{position:absolute;inset:0;background:linear-gradient(180deg,rgba(10,31,43,.25),rgba(10,31,43,.88))}
  .equipo h3,.equipo p,.equipo .puesto-lista{position:relative;margin:0}
  .equipo .puesto-lista{
    font-family:var(--dato);font-size:11px;letter-spacing:.2em;
    color:var(--arena);text-transform:uppercase;margin-bottom:8px;
  }
  .equipo h3{
    font-family:var(--display);text-transform:uppercase;font-weight:600;
    font-size:clamp(22px,3.4vw,30px);line-height:1.05;
  }
  .equipo p{margin-top:8px;color:rgba(242,240,233,.88);font-size:15px}
 
  footer{
    padding:32px 0 56px;font-family:var(--dato);font-size:12px;
    letter-spacing:.14em;text-transform:uppercase;color:rgba(242,240,233,.55);
  }
 
  @media (max-width:900px){
    .tarjetas{grid-template-columns:repeat(2,minmax(0,1fr))}
  }
  @media (max-width:860px){
    .series{grid-template-columns:1fr}
  }
  @media (max-width:760px){
    .tarjetas{grid-template-columns:1fr}
    .equipos{grid-template-columns:1fr}
    .dato{border-right:0;border-bottom:1px solid rgba(242,240,233,.12);flex:1 1 100%}
    .dato:last-child{border-bottom:0}
    section{padding:56px 0}
    .menu ul{gap:16px}
  }
  @media (prefers-reduced-motion:reduce){
    *{animation:none !important;transition:none !important}
    html{scroll-behavior:auto}
  }
</style>
</head>
<body>
 
<nav class="menu" aria-label="Secciones">
  <ul>
    <li><a href="#presentacion">Manuel Otaiza</a></li>
    <li><a href="#hobbies">Mis hobbies</a></li>
    <li><a href="#series">Mis series</a></li>
    <li><a href="#peliculas">Mis películas</a></li>
    <li><a href="#futbol">Fútbol y equipos</a></li>
  </ul>
</nav>
 
<header class="portada" id="presentacion">
  <svg class="lineas" viewBox="0 0 1000 500" preserveAspectRatio="none" aria-hidden="true">
    <g fill="none" stroke="#F2F0E9" stroke-width="2">
      <rect x="2" y="2" width="996" height="496"/>
      <line x1="500" y1="0" x2="500" y2="500"/>
      <circle cx="500" cy="250" r="90"/>
      <rect x="2" y="150" width="120" height="200"/>
      <rect x="878" y="150" width="120" height="200"/>
    </g>
  </svg>
  <div class="envoltura">
    <p class="rotulo">Mi presentación</p>
    <h1 class="nombre">
      <span>Manuel</span>
      <span class="apellido">Otaiza</span>
    </h1>
    <p class="bajada">
      Soy chileno y estudiante de Ingeniería en Informática, ya en el último año de la carrera.
      Fuera de los ramos, el tiempo se me va entre la pelota, la pesca, la familia y una buena serie.
    </p>
 
    <div class="porque">
      <h2>¿Por qué elegí informática?</h2>
      <p>
        La verdad es que empezó en la media: veía videos de
        <a href="https://www.instagram.com/naschurmann/?hl=es" target="_blank" rel="noopener">Nicolás Schürmann</a>,
        que era desarrollador, y de ahí le empecé a agarrar cariño al área. Lo que partió como
        curiosidad terminó siendo la carrera que estoy a punto de terminar.
      </p>
    </div>
    <dl class="datos">
      <div class="dato"><dt>País</dt><dd>Chile</dd></div>
      <div class="dato"><dt>Carrera</dt><dd>Ing. Informática</dd></div>
      <div class="dato"><dt>Etapa</dt><dd>Último año</dd></div>
      <div class="dato"><dt>Colores</dt><dd>La U · Barcelona</dd></div>
    </dl>
  </div>
</header>
 
<main>
 
  <section id="hobbies">
    <div class="envoltura">
      <h2 class="titulo">Mis hobbies</h2>
      <p class="subtitulo">Lo que hago cuando no estoy estudiando.</p>
 
      <div class="tarjetas">
        <article class="tarjeta" style="animation-delay:.05s">
          <p class="etiqueta">Aire libre</p>
          <h3>La pesca</h3>
          <p>El panorama más tranquilo de todos: preparar el equipo, tirar la línea y esperar. Sirve para desconectarse un rato del computador y de la ciudad.</p>
        </article>
        <article class="tarjeta" style="animation-delay:.12s">
          <p class="etiqueta">Los míos</p>
          <h3>La familia</h3>
          <p>Pasar tiempo con mi familia es lo que más ordena la semana. Un almuerzo largo o una tarde sin apuro vale por cualquier otro plan.</p>
        </article>
        <article class="tarjeta" style="animation-delay:.19s">
          <p class="etiqueta">Cancha</p>
          <h3>El fútbol</h3>
          <p>Verlo y jugarlo. Es el tema del que puedo hablar sin cansarme y el que me hace revisar los resultados apenas termina la fecha.</p>
        </article>
        <article class="tarjeta" style="animation-delay:.26s">
          <p class="etiqueta">Pantalla</p>
          <h3>Los videojuegos</h3>
          <p>Lo que más juego en la semana, solo o en línea con amigos. También es parte de la razón por la que terminé metido en la informática.</p>
        </article>
        <article class="tarjeta" style="animation-delay:.33s">
          <p class="etiqueta">Sonido</p>
          <h3>La música</h3>
          <p>Suena mientras estudio, mientras programo y mientras hago cualquier otra cosa. Es lo que arma el resto del día.</p>
        </article>
      </div>
    </div>
  </section>
 
  <section id="series">
    <div class="envoltura">
      <h2 class="titulo">Mis 3 series favoritas</h2>
      <p class="subtitulo">Las que recomiendo sin pensarlo dos veces.</p>
      <div class="series">
        <article class="serie">
          <p class="puesto-lista">01</p>
          <h3>Suits</h3>
          <p>Abogados, trajes y diálogos rápidos. La típica serie que empiezas por un capítulo y terminas viendo cuatro.</p>
        </article>
        <article class="serie">
          <p class="puesto-lista">02</p>
          <h3>Breaking Bad</h3>
          <p>Ver cómo Walter White se transforma capítulo a capítulo es lo mejor que le ha pasado a la televisión.</p>
        </article>
        <article class="serie">
          <p class="puesto-lista">03</p>
          <h3>Lucifer</h3>
          <p>Casos policiales con humor y un protagonista que se roba cada escena. Perfecta para ver relajado.</p>
        </article>
      </div>
    </div>
  </section>
 
  <section id="peliculas">
    <div class="envoltura">
      <h2 class="titulo">Mis 3 películas favoritas</h2>
      <p class="subtitulo">Las que puedo repetir cuando sea.</p>
      <div class="series">
        <article class="serie">
          <p class="puesto-lista">01</p>
          <h3>Hasta el último hombre</h3>
          <p>Una historia real de guerra que se sostiene sola. De esas que te dejan pensando un buen rato después de los créditos.</p>
        </article>
        <article class="serie">
          <p class="puesto-lista">02</p>
          <h3>Son como niños</h3>
          <p>Puro humor y amigos de toda la vida. Perfecta para ver acompañado y reírse sin complicarse.</p>
        </article>
        <article class="serie">
          <p class="puesto-lista">03</p>
          <h3>¿Qué pasó ayer?</h3>
          <p>Toda la saga, no solo la primera. Cada una tiene su desorden y funciona igual de bien.</p>
        </article>
      </div>
    </div>
  </section>
 
  <section id="futbol">
    <div class="envoltura">
      <h2 class="titulo">Fútbol y equipos</h2>
      <p class="subtitulo">
        Me gusta mucho el fútbol: verlo y jugarlo. Podría decirse que soy fanático de mis dos equipos,
        así que entre la liga chilena y la española siempre hay un partido esperando.
      </p>
      <div class="equipos">
        <div class="equipo equipo--azul">
          <div class="franjas"></div><div class="velo"></div>
          <p class="puesto-lista">Chile</p>
          <h3>Universidad de Chile</h3>
          <p>Mi equipo acá. Los partidos se ven sin importar el día ni la hora, y los clásicos se sufren completos.</p>
        </div>
        <div class="equipo equipo--blaugrana">
          <div class="franjas"></div><div class="velo"></div>
          <p class="puesto-lista">España</p>
          <h3>FC Barcelona</h3>
          <p>El equipo que sigo en Europa. Me gusta el juego de toque y salir jugando desde atrás.</p>
        </div>
      </div>
    </div>
  </section>
 
</main>
 
<footer>
  <div class="envoltura">Manuel Otaiza · Chile · 2026</div>
</footer>
 
</body>
</html>
 
