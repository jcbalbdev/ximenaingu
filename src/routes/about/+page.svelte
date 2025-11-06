<script lang="ts">
  import bg from '$lib/images/ximenaflorayfauna.png'; // usa tu imagen grande de fondo

  // Párrafos que irán rotando
  const paragraphs = [
    'Ximena Ingu es una cantautora peruana que mezcla folk y pop electrónico. Sus letras exploran la naturaleza, la ciudad y la nostalgia.',
    'En vivo, su música apuesta por la cercanía: melodías íntimas, coros memorables y paisajes sonoros con texturas analógicas y digitales.',
    '“Flora y Fauna” es su proyecto más reciente: un viaje por emociones cotidianas, donde lo simple se vuelve profundo.',
    'Ximena compone desde la honestidad. Cada canción inicia con una imagen: una caminata, un susurro, el eco del mar en Barranco.'
  ];

  let i = 0;                // índice del párrafo actual
  let playing = true;       // estado de reproducción
  const intervalMs = 6000;  // tiempo entre cambios

  let timer: number | undefined;

  function play() {
    if (playing) return;
    playing = true;
    startTimer();
  }
  function pause() {
    playing = false;
    stopTimer();
  }
  function toggle() {
    playing ? pause() : play();
  }
  function next() {
    i = (i + 1) % paragraphs.length;
  }
  function prev() {
    i = (i - 1 + paragraphs.length) % paragraphs.length;
  }

  function startTimer() {
    stopTimer();
    timer = window.setInterval(() => {
      if (playing) next();
    }, intervalMs);
  }
  function stopTimer() {
    if (timer) {
      clearInterval(timer);
      timer = undefined;
    }
  }

  import { onMount, onDestroy } from 'svelte';
  onMount(startTimer);
  onDestroy(stopTimer);

  // Accesos con teclado: espacio = play/pausa, flechas = prev/next
  function onKey(e: KeyboardEvent) {
    if (e.code === 'Space') { e.preventDefault(); toggle(); }
    else if (e.key === 'ArrowRight') next();
    else if (e.key === 'ArrowLeft') prev();
  }
</script>

<svelte:head>
  <title>About — Ximena Ingu</title>
  <meta name="description" content="Sección about interactiva con controles tipo reproductor." />
</svelte:head>

<section class="about" on:keydown={onKey} tabindex="0" aria-label="Sección About con reproductor de texto">
  <!-- Fondo -->
  <img class="bg" src={bg} alt="" aria-hidden="true" />
  

  <!-- Encabezados esquineros (opcional) -->
  

  <!-- Círculo amarillo posterior (estilo póster) -->
  

  <!-- Contenido principal -->
  <div class="content">
		<div class="corners">
    <p class="tiny left">Singer & Songwriter</p>
    <p class="tiny right">Desde 2021</p>
  </div>
    <h1 class="title">
      <span>XIMENA INGU</span>
    </h1>

    <!-- Reproductor de texto -->
    <div class="player">
      <button class="btn" on:click={prev} aria-label="Párrafo anterior" title="Anterior (←)">
        <!-- icon prev -->
        <svg viewBox="0 0 24 24" width="22" height="22" aria-hidden="true"><path d="M6 6h2v12H6zM20 6v12l-10-6 10-6z" fill="currentColor"/></svg>
      </button>

      <button class="btn play" on:click={toggle} aria-pressed={playing} aria-label={playing ? 'Pausar' : 'Reproducir'} title="Espacio para {playing ? 'pausar' : 'reproducir'}">
        {#if playing}
          <!-- icon pause -->
          <svg viewBox="0 0 24 24" width="26" height="26" aria-hidden="true"><path d="M6 5h4v14H6zm8 0h4v14h-4z" fill="currentColor"/></svg>
        {:else}
          <!-- icon play -->
          <svg viewBox="0 0 24 24" width="26" height="26" aria-hidden="true"><path d="M8 5v14l11-7z" fill="currentColor"/></svg>
        {/if}
      </button>

      <button class="btn" on:click={next} aria-label="Párrafo siguiente" title="Siguiente (→)">
        <!-- icon next -->
        <svg viewBox="0 0 24 24" width="22" height="22" aria-hidden="true"><path d="M16 6h2v12h-2zM4 6v12l10-6L4 6z" fill="currentColor"/></svg>
      </button>
    </div>

    <!-- Texto rotatorio -->
    <p class="paragraph" role="status" aria-live="polite">{paragraphs[i]}</p>

    <!-- Indicadores -->
    <div class="dots" aria-hidden="true">
      {#each paragraphs as _, idx}
        <span class:active={idx === i}></span>
      {/each}
    </div>
  </div>
</section>

<style>
  :global(body){ margin:0; }

  .about{
    --ink:#0b1230;
    --text:#ffffff;
    --muted:#8a8a8a;
    --accent:#f1b432;
		--card-grad-from: #ff7043;
    --card-grad-to: violet;

    position: relative;
    min-height: 100vh;
    background: var(--ink);
    color: var(--text);
    overflow: hidden;

    display: grid;
    place-items: end start;
    padding: clamp(16px, 4vw, 40px);
		border-radius: 24px;
  }


  /* Fondo */
.bg{
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: contain;       /* antes: cover */
  object-position: right;   /* centra la imagen */
  background: #111;       /* color de “letterbox” en los bordes */
  z-index: 1;
  filter: none;              /* opcional: evita oscurecer la imagen original */
}
  .overlay{
    position: absolute; inset: 0;
    background: linear-gradient(180deg, var(--card-grad-from) 0%, var(--card-grad-to) 100%);
    z-index: 0;
  }
  /* Esquineros */
  .corners .tiny{
    position: absolute;
    top: 18px;
    font: 600 12px/1.2 Inter, system-ui, sans-serif;
    color: var(--muted);
    margin: 0;
  }
  .corners .tiny.left{ left: 20px; }
  .corners .tiny.right{ right: 20px; text-align: right; }

  /* Contenido */
  .content{
    position: relative;
    z-index: 2;
    max-width: 900px;
    padding: clamp(12px, 4vw, 24px);
    margin-left: clamp(12px, 8vw, 10px);
    margin-bottom: clamp(24px, 8vh, 90px);
		/* background-color: tomato; */
  }

  .title{
    margin: 0 0 12px;
    font: 800 clamp(40px, 8vw, 96px)/0.95 Inter, system-ui, sans-serif;
    letter-spacing: -0.5px;
  }

  /* Reproductor */
  .player{
    display: inline-flex;
    align-items: center;
    gap: 10px;
    margin: 8px 0 12px;
    backdrop-filter: blur(4px);
  }
  .btn{
    display: grid; place-items: center;
    width: 44px; height: 44px;
    border-radius: 12px;
    border: 1px solid rgba(255,255,255,.18);
    background: rgba(255,255,255,.1);
    color: #fff;
    cursor: pointer;
    transition: transform .08s ease, background .2s ease;
  }
  .btn:hover{ background: rgba(255,255,255,.18); }
  .btn:active{ transform: scale(.98); }
  .btn.play{
    width: 56px; height: 56px; border-radius: 16px;
    border-width: 1.5px;
  }

  /* Párrafo dinámico */
  .paragraph{
    max-width: 60ch;
    font: 500 clamp(14px, 1.6vw, 18px)/1.7 Inter, system-ui, sans-serif;
    color: #e8ebff;
    margin: 0;
  }

  /* Indicadores */
  .dots{
    display: flex; gap: 8px; margin-top: 12px;
  }
  .dots span{
    width: 8px; height: 8px; border-radius: 50%;
    background: rgba(255,255,255,.35);
  }
  .dots span.active{ background: #fff; }

  /* Responsive */
  @media (max-width: 900px){
    .content{
      margin-left: 0;
      margin-bottom: clamp(18px, 10vh, 64px);
    }
    .title{
      text-align: left;
      font-size: clamp(34px, 10vw, 64px);
    }
    .paragraph{ max-width: 100%; }
    .sun{
      left: 50%;
      transform: translateX(-50%);
      bottom: 32%;
      opacity: .8;
    }
  }
</style>
