
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
            <<div class="card" data-index="1" style="background:white;padding:10px"><img src="Música snoppy.png" alt="Música snoppy" style="max-width:100%;max-height:100%;object-fit:contain;border-radius:10px"></div>
            <div class="card" data-index="2" style="background:white;padding:10px"><img src="carta de snoppy.png" alt="carta de snoppy" style="max-width:100%;max-height:100%;object-fit:contain;border-radius:10px"></div>
          </div>
        </div>
      </div>
    </section>

    <!-- Página sorpresa que desliza desde abajo -->
    <div class="surprise" id="surprise">
      <div class="box">
        <h2>¡Sorpresa!</h2>
        <p>Gracias por seguir las pistas. Te quiero mucho ❤️</p>
        <p style="font-size:13px;color:#7a7a7a;margin-top:10px">Puedes editar este mensaje desde el código.</p>
      </div>
    </div>
  </main>

  <script>
    // Valor del código correcto: cámbialo aquí según quieras
    const SECRET_CODE = '23/11/2024'; // <- editar aquí si quieres otro código (no distingue mayúsculas/minusculas)

    const openBtn = document.getElementById('openBtn');
    const codeArea = document.getElementById('codeArea');
    const checkBtn = document.getElementById('checkBtn');
    const codeInput = document.getElementById('codeInput');
    const carouselWrap = document.getElementById('carouselWrap');
    const track = document.getElementById('track');
    const surprise = document.getElementById('surprise');

    openBtn.addEventListener('click', ()=>{
      openBtn.style.display='none';
      codeArea.style.display='flex';
      codeInput.focus();
    });

    checkBtn.addEventListener('click', ()=>{
      const val = (codeInput.value || '').trim().toUpperCase();
      if(val === SECRET_CODE.toUpperCase()){
        // mostrar carousel
        codeArea.style.display='none';
        carouselWrap.style.display='block';
        // opcional: pausa la animación autom. cuando el usuario mueve el ratón
        track.addEventListener('mouseenter', ()=> track.style.animationPlayState='paused');
        track.addEventListener('mouseleave', ()=> track.style.animationPlayState='running');
      } else {
        // pequeño efecto de error
        codeInput.classList.add('squash');
        setTimeout(()=> codeInput.classList.remove('squash'),400);
        codeInput.value='';
        codeInput.placeholder = 'Código incorrecto, inténtalo de nuevo';
      }
    });

    // Al pulsar Enter en el campo
    codeInput.addEventListener('keyup',(e)=>{ if(e.key === 'Enter') checkBtn.click(); });

    // Al hacer clic en cualquier tarjeta: efecto 'aplastar' y mostrar sorpresa
    document.querySelectorAll('.card').forEach(card => {
      card.addEventListener('click', ()=>{
        card.style.transformOrigin = 'center bottom';
        card.animate([
          { transform: 'scale(1)' },
          { transform: 'scale(1.05,0.6)' },
          { transform: 'scale(1)' }
        ],{ duration:450, easing:'ease' });

        // después de efecto, desliza la página sorpresa
        setTimeout(()=>{
          surprise.classList.add('show');
          // detén la animación del track
          track.style.animationPlayState='paused';
        },460);
      });
    });

    // Para probar rápidamente en escritorio: permite avanzar a sorpresa con tecla S
    document.addEventListener('keydown',(e)=>{ if(e.key.toLowerCase()==='s'){ surprise.classList.add('show'); } });
  </script>
</body>
</html>
