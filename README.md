<html lang="es">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Página sorpresa</title>
<style>
:root{--bg:#fff7f8;--accent:#e64a6b;--muted:#6b6b6b}
html,body{height:100%;margin:0;font-family:Inter, system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial}
.stage{height:100vh;display:flex;align-items:center;justify-content:center;background:linear-gradient(180deg,#fff 0%, #fff7f8 100%);overflow:hidden}

/* Intro */
.intro{position:relative;width:90%;max-width:760px;padding:40px;border-radius:18px;background:rgba(255,255,255,0.9);box-shadow:0 8px 30px rgba(0,0,0,0.08);text-align:center}
.heart-svg{width:180px;height:180px;margin:0 auto 20px;filter:drop-shadow(0 8px 20px rgba(230,74,107,0.18))}
h1{font-size:28px;margin:6px 0;color:var(--accent)}
p.lead{margin:0 0 18px;color:var(--muted)}
button.btn{background:var(--accent);color:white;border:0;padding:12px 20px;border-radius:12px;font-weight:600;cursor:pointer}

/* Code screen */
.code-area{margin-top:18px;display:none;gap:10px;justify-content:center;align-items:center}
.code-input{padding:12px 16px;border-radius:12px;border:2px solid rgba(0,0,0,0.06);font-size:16px;width:180px;text-align:center}
.hint{font-size:13px;color:#999;margin-top:10px}

/* Carousel */
.carousel-wrap{position:relative;width:100%;max-width:880px;margin:28px auto;display:none}
.carousel{overflow:hidden;border-radius:14px;height:220px;background:linear-gradient(90deg,#fff,#fff0f2)}
.track{display:flex;gap:16px;padding:18px;will-change:transform;animation:slide 12s linear infinite}
.card{min-width:260px;height:160px;border-radius:12px;display:flex;align-items:center;justify-content:center;font-weight:700;font-size:18px;user-select:none;cursor:pointer;box-shadow:0 6px 22px rgba(0,0,0,0.07);transition:transform .18s ease}
.card:active{transform:scale(.98)}

@keyframes slide{
  0%{transform:translateX(0)}
  33%{transform:translateX(-276px)}
  66%{transform:translateX(-552px)}
  100%{transform:translateX(0)}
}

/* squash animation */
.squash{animation:squash .45s ease forwards}
@keyframes squash{0%{transform:scale(1)}50%{transform:scale(1.05,0.75)}100%{transform:scale(1,1)}}

/* Slide to surprise */
.surprise{position:fixed;inset:0;background:linear-gradient(180deg,#fff7f8,#ffeef4);display:flex;align-items:center;justify-content:center;flex-direction:column;transform:translateY(110vh);transition:transform .7s cubic-bezier(.22,1,.36,1)}
.surprise.show{transform:translateY(0)}
.surprise .box{background:white;padding:28px;border-radius:18px;box-shadow:0 18px 50px rgba(230,74,107,0.12);text-align:center}
.surprise h2{color:var(--accent);margin:0 0 8px}
.surprise p{color:var(--muted);margin:0 0 12px}

/* small */
@media (max-width:600px){.track{padding:12px}.card{min-width:200px}}

/* Reproductor estilo dibujo debajo */
.player-dibujo {
  width:10cm;
  height:5cm;
  background:#fff0f2;
  border:3px dashed #e64a6b;
  border-radius:12px;
  display:flex;
  flex-direction:column;
  justify-content:center;
  align-items:center;
  box-shadow:0 6px 16px rgba(230,74,107,0.3);
  margin-top:15px;
}
.player-dibujo audio {
  width:90%;
  border-radius:8px;
}
.play-icon {
  width:30px;
  height:30px;
  margin-bottom:8px;
  clip-path: polygon(0% 0%, 100% 50%, 0% 100%);
  background:#e64a6b;
}

/* BUZÓN */
.buzon-container{position:relative;width:300px;height:200px;margin:20px auto;text-align:center;}
.buzon{width:100%; height:100%; background:#e64a6b; border-radius:12px; display:flex; flex-direction:column; align-items:center; justify-content:flex-start; cursor:pointer; position:relative; overflow:hidden;}
.buzon h3{color:white; font-size:22px; margin:10px 0;}
.tarjeta-cerrada{width:100px; height:60px; background:#fff0f2; border:2px dashed #fff; border-radius:6px; margin-top:20px; cursor:pointer; transition:transform 0.7s;}
.tarjeta-abierta{position:absolute; top:50px; left:50%; transform:translateX(-50%) scale(0); width:320px; height:160px; display:flex; border-radius:12px; overflow:hidden; box-shadow:0 8px 20px rgba(0,0,0,0.2); transition:transform 0.7s;}
.tarjeta-abierta .lado{width:50%; height:100%; display:flex; justify-content:center; align-items:center;}
.tarjeta-abierta .lado.foto img{width:100%; height:100%; object-fit:cover;}
.tarjeta-abierta .lado.texto{background:#fff; padding:10px; font-size:14px; text-align:center;}

/* BOTÓN VOLVER */
.backBtn{display:flex; align-items:center; gap:6px; background-color:#f8c8d8; color:#fff; border:none; padding:6px 12px; border-radius:8px; font-size:14px; cursor:pointer; margin:20px auto;}
.backBtn span{display:inline-block; transform:rotate(180deg); font-weight:bold; font-size:16px;}
</style>
</head>
<body>
<main class="stage">
<section class="intro" id="intro">
<img class="heart-svg" src="Snoppy.png" alt="Snoopy con corazón" />
<h1>Tienes un mensaje 💌</h1>
<p class="lead">Haz clic en abrir y sigue las pistas para ver la sorpresa.</p>

<div style="display:flex;gap:10px;justify-content:center;align-items:center;flex-direction:column">
  <button class="btn" id="openBtn">Abrir</button>
  <div class="code-area" id="codeArea">
    <input class="code-input" id="codeInput" placeholder="Ingresa el código" aria-label="Código" />
    <button class="btn" id="checkBtn">Enviar</button>
  </div>
  <div class="hint">Pista: Es una fecha muy importante para los dos.</div>
</div>

<!-- Carousel oculto inicialmente -->
<div class="carousel-wrap" id="carouselWrap">
  <div class="carousel" aria-hidden="false">
    <div class="track" id="track">
      <div class="card" data-index="1" style="background:white;padding:10px"><img src="sonido.png" alt="sonido" style="max-width:100%;max-height:100%;object-fit:contain;border-radius:10px"></div>
      <div class="card" data-index="2" style="background:white;padding:10px"><img src="carta.png" alt="carta" style="max-width:100%;max-height:100%;object-fit:contain;border-radius:10px"></div>
    </div>
  </div>
</div>
</section>

<!-- Página sorpresa sonido -->
<div class="surprise" id="surpriseSonido" style="display:none;">
  <div style="display:flex; gap:15px; justify-content:center; align-items:stretch; flex-wrap:wrap; max-width:600px; margin:auto; position:relative; z-index:10;">
    <div class="box" style="width:45%; text-align:center;min-height:400px;">
      <img src="foto.png" alt="Imagen sorpresa" style="width:100%; max-height:400px; object-fit:cover; border-radius:12px; position:relative; z-index:10;">
    </div>
    <div class="box" style="width:45%; text-align:center; min-height:400px;">
      <video src="tocadiscos.mp4" autoplay loop muted style="width:100%; height:400px; border-radius:12px; object-fit:cover; background:black; position:relative; z-index:10;"></video>
    </div>
  </div>
  <div class="player-dibujo" style="width:200px; height:100px; margin:20px auto; padding:10px; border:2px dashed #e64a6b; border-radius:12px; display:flex; flex-direction:column; align-items:center; justify-content:center; background:#fff0f2;">
    <div class="play-icon" style="width:30px; height:30px; background:#e64a6b; clip-path: polygon(0 0, 100% 50%, 0 100%); margin-bottom:8px;"></div>
    <audio src="lala.mp3" controls style="width:90%; height:30px;"></audio>
  </div>
  <button class="backBtn"><span>&#10148;</span> Volver</button>
</div>

<!-- Página sorpresa carta con buzón -->
<div class="surprise" id="surpriseCarta" style="display:none;">
  <div class="buzon-container">
    <div class="buzon" id="buzon">
      <h3>BUZÓN</h3>
      <div class="tarjeta-cerrada" id="tarjetaCerrada"></div>
    </div>
    <div class="tarjeta-abierta" id="tarjetaAbierta">
      <div class="lado foto"><img src="foto.png"></div>
      <div class="lado texto"><p>¡Aquí está tu mensaje secreto!</p></div>
      <button onclick="cerrarTarjeta()" style="position:absolute; bottom:5px; right:5px; padding:4px 8px; background:#e64a6b; color:white; border:none; border-radius:6px; cursor:pointer;">Cerrar</button>
    </div>
  </div>
  <button class="backBtn"><span>&#10148;</span> Volver</button>
</div>

</main>

<script>
const SECRET_CODE = '23/11/2024';
const openBtn = document.getElementById('openBtn');
const codeArea = document.getElementById('codeArea');
const checkBtn = document.getElementById('checkBtn');
const codeInput = document.getElementById('codeInput');
const carouselWrap = document.getElementById('carouselWrap');
const track = document.getElementById('track');

const surpriseSonido = document.getElementById('surpriseSonido');
const surpriseCarta = document.getElementById('surpriseCarta');

// Tarjeta buzón
const tarjetaAbierta = document.getElementById('tarjetaAbierta');
const tarjetaCerrada = document.getElementById('tarjetaCerrada');
const buzon = document.getElementById('buzon');

openBtn.addEventListener('click', ()=>{
  openBtn.style.display='none';
  codeArea.style.display='flex';
  codeInput.focus();
});

checkBtn.addEventListener('click', ()=>{
  const val = (codeInput.value || '').trim().toUpperCase();
  if(val === SECRET_CODE.toUpperCase()){
    codeArea.style.display='none';
    carouselWrap.style.display='block';
    track.addEventListener('mouseenter', ()=> track.style.animationPlayState='paused');
    track.addEventListener('mouseleave', ()=> track.style.animationPlayState='running');
  } else {
    codeInput.classList.add('squash');
    setTimeout(()=> codeInput.classList.remove('squash'),400);
    codeInput.value='';
    codeInput.placeholder = 'Código incorrecto, inténtalo de nuevo';
  }
});

codeInput.addEventListener('keyup',(e)=>{ if(e.key === 'Enter') checkBtn.click(); });

// Click en tarjetas
document.querySelectorAll('.card').forEach(card => {
  card.addEventListener('click', ()=>{
    if(card.dataset.index === "1"){ // tarjeta sonido
      card.style.transformOrigin = 'center bottom';
      card.animate([{ transform: 'scale(1)' },{ transform: 'scale(1.05,0.6)' },{ transform: 'scale(1)' }],{ duration:450, easing:'ease' });
      setTimeout(()=>{
        surpriseSonido.style.display = 'flex';
        surpriseSonido.classList.add('show');
        carouselWrap.style.display = 'none';
        track.style.animationPlayState='paused';
      },460);
    } else if(card.dataset.index === "2"){ // tarjeta carta
      surpriseCarta.style.display = 'flex';
      surpriseCarta.classList.add('show');
      carouselWrap.style.display = 'none';
      track.style.animationPlayState='paused';
    }
  });
});

// Botón volver
document.querySelectorAll('.backBtn').forEach(btn => {
  btn.addEventListener('click', ()=>{
    surpriseSonido.style.display = 'none';
    surpriseCarta.style.display = 'none';
    carouselWrap.style.display = 'block';
    track.style.animationPlayState='running';
    setTimeout(()=>{carouselWrap.scrollIntoView({behavior:'smooth'});},50);
  });
});

// Funciones buzón
buzon.addEventListener('click', ()=>{
  tarjetaAbierta.style.transform = 'translateY(-220px) scale(1)';
  tarjetaCerrada.style.transform = 'translateY(-300px) scale(0)';
});

function cerrarTarjeta() {
  tarjetaAbierta.style.transform = 'translateY(0) scale(0)';
  tarjetaCerrada.style.transform = 'translateY(0) scale(1)';
}
</script>
</body>
</html>
