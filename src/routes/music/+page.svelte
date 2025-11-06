<script lang="ts">
  import { onMount, onDestroy } from 'svelte';
  import flora from '$lib/images/florayfaunaFINAL.jpg';
  import tren from '$lib/images/eltren.png';
  import desaparecer from '$lib/images/desaparecer.png';

  // Canciones
  const songs = [
    { title: 'El Tren – Single',       year: 2024, cover: tren,        link: 'https://open.spotify.com/track/5YYNW4xC5fPQhGEjyDRyfT' },
    { title: 'Flora y Fauna – Single', year: 2024, cover: flora,       link: 'https://open.spotify.com/track/2Hr06BCw7FiqElxJscmSlL' },
    { title: 'Des-aparecer – Single',  year: 2023, cover: desaparecer, link: 'https://open.spotify.com/track/72wK2iEJjD9GqWCSqNjhsA' },
		{ title: 'El Tren – Single',       year: 2024, cover: tren,        link: 'https://open.spotify.com/track/5YYNW4xC5fPQhGEjyDRyfT' },
		{ title: 'Flora y Fauna – Single', year: 2024, cover: flora,       link: 'https://open.spotify.com/track/2Hr06BCw7FiqElxJscmSlL' },
		{ title: 'Des-aparecer – Single',  year: 2023, cover: desaparecer, link: 'https://open.spotify.com/track/72wK2iEJjD9GqWCSqNjhsA' }
  ];

  let rowEl: HTMLDivElement;

  // Flechas (scroll casi una “pantalla” por clic)
  function scrollNext() {
    if (!rowEl) return;
    rowEl.scrollBy({ left: rowEl.clientWidth * 0.9, behavior: 'smooth' });
  }
  function scrollPrev() {
    if (!rowEl) return;
    rowEl.scrollBy({ left: -rowEl.clientWidth * 0.9, behavior: 'smooth' });
  }

  // Auto-scroll suave
  const SPEED_PX = 1.2;
  const TICK_MS = 18;
  let autoTimer: number | undefined;

  function startAuto() {
    stopAuto();
    autoTimer = window.setInterval(() => {
      if (!rowEl) return;
      const { scrollLeft, scrollWidth, clientWidth } = rowEl;
      if (scrollLeft + clientWidth >= scrollWidth - 1) {
        rowEl.scrollTo({ left: 0, behavior: 'auto' });
      } else {
        rowEl.scrollLeft = scrollLeft + SPEED_PX;
      }
      updateEdges();
    }, TICK_MS);
  }

  function stopAuto() {
    if (autoTimer) {
      clearInterval(autoTimer);
      autoTimer = undefined;
    }
  }

  // Deshabilitar flechas al llegar a extremos
  let atStart = true;
  let atEnd = false;
  function updateEdges() {
    if (!rowEl) return;
    const { scrollLeft, scrollWidth, clientWidth } = rowEl;
    atStart = scrollLeft <= 2;
    atEnd = scrollLeft + clientWidth >= scrollWidth - 2;
  }

  onMount(() => {
    updateEdges();
    const handler = () => updateEdges();
    rowEl?.addEventListener('scroll', handler, { passive: true });
    startAuto();
    return () => {
      rowEl?.removeEventListener('scroll', handler);
      stopAuto();
    };
  });

  // Pausar auto-scroll mientras el usuario interactúa
  const pauseAuto = () => stopAuto();
  const resumeAuto = () => startAuto();
</script>

<svelte:head>
  <title>Música — Ximena Ingu</title>
  <meta name="description" content="Canciones y singles de Ximena Ingu" />
</svelte:head>

<section class="music" aria-label="Carrusel de singles">
  <h1 class="section-title">Singles y EP</h1>

  <div class="carousel">
    <!-- retroceder -->
    <button
      class="nav nav-left"
      on:click={scrollPrev}
      on:mouseenter={pauseAuto}
      on:mouseleave={resumeAuto}
      aria-label="Retroceder"
      disabled={atStart}
    >
      <svg viewBox="0 0 24 24" width="18" height="18" aria-hidden="true">
        <path d="M6 6h2v12H6zM20 6v12l-10-6 10-6z" fill="currentColor"/>
      </svg>
    </button>

    <!-- fila -->
    <div
      class="row"
      bind:this={rowEl}
      on:mouseenter={pauseAuto}
      on:mouseleave={resumeAuto}
    >
      {#each songs as song}
        <a class="card" href={song.link} target="_blank" rel="noopener noreferrer">
          <div class="cover">
            <img src={song.cover} alt={`Portada de ${song.title}`} />
            <div class="overlay">
              <svg viewBox="0 0 24 24" class="play-icon" aria-hidden="true">
                <path d="M8 5v14l11-7z" fill="currentColor" />
              </svg>
            </div>
          </div>
          <div class="info">
            <p class="title">{song.title}</p>
            <p class="year">{song.year}</p>
          </div>
        </a>
      {/each}
    </div>

    <!-- avanzar -->
    <button
      class="nav nav-right"
      on:click={scrollNext}
      on:mouseenter={pauseAuto}
      on:mouseleave={resumeAuto}
      aria-label="Avanzar"
      disabled={atEnd}
    >
      <svg viewBox="0 0 24 24" width="18" height="18" aria-hidden="true">
        <path d="M16 6h2v12h-2zM4 6v12l10-6L4 6z" fill="currentColor"/>
      </svg>
    </button>
  </div>
</section>

<style>
  .music{
    max-width:1300px;
    margin:0 auto;
    padding:clamp(24px,5vw,60px);
    
    font-family:Inter,system-ui,sans-serif;
  }

  .section-title{
    font-size:clamp(22px,3vw,28px);
    font-weight:700;
    margin-bottom:16px;
		color:#111;
  }

  /* Carrusel */
  .carousel{ position:relative; }

  .row{
    display:flex;
    gap:24px;
    overflow-x:auto;
    overflow-y:hidden;
    padding:10px 2px 6px;
    scroll-snap-type:x mandatory;
    scroll-padding-left:2px;
    -webkit-overflow-scrolling:touch;
  }

  /* ocultar scrollbar */
  .row::-webkit-scrollbar{ height:0; }
  .row{ scrollbar-width:none; }

  /* === Tarjeta: 3 visibles en pantallas grandes === */
  .card{
    flex:0 0 auto;
    width:calc((100% - 2 * 24px) / 3);
    color:inherit;
    text-decoration:none;
    scroll-snap-align:start;
    transition:transform .2s ease;
  }
  .card:hover{ transform:scale(1.02); }

  /* Portada */
  .cover{
    position:relative;
    border-radius:10px;
    overflow:hidden;
    aspect-ratio:1/1;
    background:#1a1a1a;
  }
  .cover img{
    width:100%;
    height:100%;
    object-fit:cover;
    display:block;
    transition:opacity .3s ease;
  }
  .overlay{
    position:absolute;
    inset:0;
    display:grid;
    place-items:center;
    background:rgba(0,0,0,.6);
    opacity:0;
    transition:opacity .25s ease;
  }
  .play-icon{
    width:48px;
    height:48px;
    color:#fff;
    transition:transform .25s ease;
  }
  .cover:hover .overlay{ opacity:1; }
  .cover:hover .play-icon{ transform:scale(1.1); }

  /* Info */
  .info{ margin-top:10px; text-align:center; }
  .title{ font-size:15px; font-weight:500; color:#111; margin:0 0 4px; }
  .year{ font-size:13px; color:#aaa; margin:0; }

  /* Flechas estilo reproductor */
  .nav{
    position:absolute;
    top:50%;
    transform:translateY(-50%);
    z-index:2;
    width:46px;
    height:46px;
    display:grid;
    place-items:center;
    background:#1e1e1e;
    color:#fff;
    border:1px solid rgba(255,255,255,.2);
    border-radius:12px;
    cursor:pointer;
    transition:background .2s ease, transform .08s ease, opacity .2s ease;
  }
  .nav:hover{ background:#2a2a2a; }
  .nav:active{ transform:translateY(-50%) scale(.98); }
  .nav:disabled{ opacity:.35; cursor:default; }
  .nav-left{ left:-4px; }
  .nav-right{ right:-4px; }

  /* === Móvil: 1 tarjeta por vista === */
  @media (max-width: 900px){
    .row{ gap:18px; }
    .card{
      width:100%;
      max-width:100%;
    }
    .title{ font-size:14px; }
    .nav{ width:42px; height:42px; border-radius:10px; }
  }
</style>
