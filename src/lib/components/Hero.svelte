<script lang="ts">
  import chill from '$lib/images/chill.jpeg';
  import flora from '$lib/images/florayfaunaFINAL.jpg';
  import tren from '$lib/images/eltren.png';
  import desaparecer from '$lib/images/desaparecer.png';

  // Texto y enlaces principales
  export let artistName = 'Ximena Ingu';
  export let headline = 'Tu sonido, hoy';
  export let subtitle =
    'Explora sus canciones, entra en su mundo y siente cada track como una historia.';
  export let spotifyArtistUrl = 'https://open.spotify.com/artist/XXXXXXXX';
  export let videoUrl = 'https://www.youtube.com/watch?v=XXXXXXXX';

  // Panel central: IDs simples de Spotify (botones de texto)
  const track1 = '5YYNW4xC5fPQhGEjyDRyfT';
  const track2 = '2Hr06BCw7FiqElxJscmSlL';
  const track3 = '72wK2iEJjD9GqWCSqNjhsA';

  let currentId = track1;
  let currentType: 'track' | 'album' | 'playlist' = 'track';
  $: embedSrc = `https://open.spotify.com/embed/${currentType}/${currentId}?utm_source=generator&theme=0`;

  // Imagen actual del panel central
  let currentBg = tren; // portada inicial

  // Cambiar canción + portada
  function setTrackAndBg(id: string) {
    currentId = id;
    if (id === track1) currentBg = tren;          // El Tren
    else if (id === track2) currentBg = flora;    // Flora y Fauna
    else if (id === track3) currentBg = desaparecer; // Des-aparecer
  }

  // Tarjeta lateral (álbum con imagen)
  export let albumTitle = 'Flora y Fauna';
  export let albumSubtitle = 'Popklore para gente sensible';
  export let albumImage = '/images/album-flora-fauna.jpg';
</script>

<section class="hero">
  <!-- Columna de texto -->
  <div class="copy">
    <h1 class="title">
      <span class="muted">{artistName}</span><br />
      {headline}
    </h1>
    <p class="lead">{subtitle}</p>

    <div class="ctas">
      <a class="btn primary" href={spotifyArtistUrl} target="_blank" rel="noopener">Escuchar en Spotify</a>
      <a class="btn ghost" href={videoUrl} target="_blank" rel="noopener">Ver videoclip</a>
    </div>
  </div>

  <!-- Panel central -->
  <div class="stage">
    <div class="panel">
      <!-- Player Spotify (arriba-izquierda) -->
      <div class="panel__player">
        <iframe
          title="Spotify player"
          src={embedSrc}
          width="100%"
          height="80"
          frameborder="0"
          allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture"
          loading="lazy"
        />
      </div>

      <!-- Botones de texto -->
      <div class="panel__buttons" role="tablist" aria-label="Elegir canción">
        <button
          class:active={currentId === track1}
          role="tab"
          aria-selected={currentId === track1}
          on:click={() => setTrackAndBg(track1)}
        >El Tren</button>

        <button
          class:active={currentId === track2}
          role="tab"
          aria-selected={currentId === track2}
          on:click={() => setTrackAndBg(track2)}
        >Flora y Fauna</button>

        <button
          class:active={currentId === track3}
          role="tab"
          aria-selected={currentId === track3}
          on:click={() => setTrackAndBg(track3)}
        >Des-aparecer</button>
      </div>

      <!-- Imagen dinámica de fondo -->
      <img class="panel__art" src={currentBg} alt="Portada actual del panel" />
    </div>
  </div>

  <!-- Tarjeta lateral (álbum con imagen) -->
  <aside class="right-card">
    <div class="album-card">
      <div class="album-card__header">
        <span class="pill">Álbum Destacado</span>
      </div>

      <div class="album-cover">
        <img src={flora} alt={`Portada del álbum ${albumTitle}`} />
        <div class="cover-overlay"></div>
        <div class="cover-badge">Nuevo</div>
      </div>

      <div class="album-card__content">
        <h3 class="album-title">“{albumTitle}”</h3>
        <p class="album-subtitle">{albumSubtitle}</p>
      </div>

      <div class="album-card__footer">
        <a class="btn-play" href={spotifyArtistUrl} target="_blank" rel="noopener">
          ▶ Escuchar en Spotify
        </a>
      </div>
    </div>
  </aside>
</section>

<style>
  .hero {
    --bg: #f6f7fb;
    --ink: #121212;
    --muted: #8a8a8a;
    --panel: #ffe24d;
    --card-grad-from: #ff7043;
    --card-grad-to: violet;

    display: grid;
    grid-template-columns: 1.2fr 1.6fr 0.8fr;
    gap: 32px;
    align-items: stretch;
    padding: clamp(28px, 5vw, 60px) 5%;
    background: rgba(250, 250, 250, 0.2);
    border-radius: 24px;
    box-shadow: 0 4px 30px rgba(0,0,0,.08);
  }
.glass {
  background: rgba(255, 255, 255, 0.06); /* transparencia */
  backdrop-filter: blur(18px);
  -webkit-backdrop-filter: blur(18px);

  border-radius: 16px;
  border: 1px solid rgba(255, 255, 255, 0.12);
  box-shadow: 0 4px 30px rgba(0, 0, 0, 0.35);
  padding: 24px;
}
  /* Texto */
  .copy { display:flex; flex-direction:column; justify-content:center; padding-right: 8px; }
  .title { margin:0 0 16px; font:700 clamp(2rem, 3vw, 3.2rem)/1.1 Inter, system-ui, sans-serif; color:#fff; }
  .title .muted { color:#fff; font-weight:400; }
  .lead { color:#fff; max-width: 42ch; margin: 0 0 24px; }
  .ctas { display:flex; gap:12px; flex-wrap: wrap; }
  .btn { display:inline-flex; align-items:center; justify-content:center; padding:12px 18px; border-radius:14px; font:600 14px/1 Inter, sans-serif; text-decoration:none; transition:.2s; }
  .btn.primary { background: rgba(0, 0, 0, 0.6); color:#fff; }
  .btn.primary:hover { background:var(--ink); color:#fff; }
  .btn.ghost { background: rgba(0, 0, 0, 0.6); color:#fff;  }
  .btn.ghost:hover { background:var(--ink); color:#fff; }

  /* Panel central */
  .stage { position:relative; }
  .panel {
    position:relative; background:var(--panel); border-radius:28px; overflow:hidden;
    min-height: 440px; box-shadow:0 6px 20px rgba(0,0,0,.12);
  }
  .panel__art { position:absolute; inset:0; width:100%; height:100%; object-fit:cover; }

  .panel__player {
    position:absolute; top:16px; left:16px; width:min(360px, 55%);
    border-radius:14px; overflow:hidden; background:#fff; box-shadow:0 4px 12px rgba(0,0,0,.18); z-index:2;
  }

  /* Botones */
  .panel__buttons {
    position:absolute; bottom:16px; right:16px;
    display:flex; gap:10px; flex-wrap: nowrap; z-index:2;
  }
  .panel__buttons button {
    border:none; background: rgba(250, 250, 250, 0.5); color:#111; font:600 12px/1 Inter, system-ui, sans-serif;
    border-radius:10px; padding:8px 12px; cursor:pointer; box-shadow:0 3px 8px rgba(0,0,0,.15);
    transition: background .2s ease, transform .1s ease;
  }
  .panel__buttons button:hover { background:#f0f0f0; transform: translateY(-1px); }
  .panel__buttons button.active,
  .panel__buttons button[aria-selected="true"] {
    background:#111; color:#fff;
  }

  /* Tarjeta lateral (álbum) */
  .right-card { display:flex; align-items:stretch; }
  .album-card {
    display:flex; flex-direction:column; gap:14px;
    background: linear-gradient(
  180deg,
  #0f0f0c 0%,
  #2d3a2d 40%,
  #6c694d 100%
);
    color:#fff; border-radius:28px; padding:20px; box-shadow:0 8px 20px rgba(0,0,0,.15); overflow:hidden;
  }
  .album-card__header { display:flex; justify-content:space-between; align-items:center; }
  .pill { background:#fff9; color:#111; font:600 11px/1 Inter, sans-serif; padding:6px 12px; border-radius:999px; }

  .album-cover {
    position:relative; border-radius:20px; overflow:hidden; aspect-ratio: 1 / 1;
    box-shadow: 0 6px 16px rgba(0,0,0,.25); background:#000;
  }
  .album-cover img {
    width:100%; height:100%; object-fit:cover; display:block; transform: scale(1.01);
  }
  .cover-overlay {
    position:absolute; inset:auto 0 0 0; height:42%;
    background: linear-gradient(180deg, rgba(0,0,0,0) 0%, rgba(0,0,0,.45) 100%);
  }
  .cover-badge {
    position:absolute; top:10px; left:10px; background:#fff; color:#111;
    font:700 11px/1 Inter, sans-serif; padding:6px 10px; border-radius:999px;
    box-shadow: 0 2px 8px rgba(0,0,0,.25);
  }

  .album-card__content { text-align:center; }
  .album-title { margin:6px 0 2px; font-size:1.15rem; font-weight:800; letter-spacing:.2px; }
  .album-subtitle { font-size:.9rem; opacity:.95; }

  .album-card__footer { display:flex; justify-content:center; }
  .btn-play {
    display:inline-flex; align-items:center; gap:8px; background:#fff; color:#111;
    font:600 14px/1 Inter, sans-serif; text-decoration:none; padding:10px 16px; border-radius:14px;
    box-shadow:0 4px 10px rgba(0,0,0,.2);
  }
  .btn-play:hover { background:#ffece6; }

  /* Responsive */
  @media (max-width: 1000px) {
    .hero { grid-template-columns: 1fr; gap: 20px; padding: 32px 20px; }
    .panel { min-height: 360px; }
    .panel__player { width: calc(100% - 32px); }
    .panel__buttons {
      top: 108px;
      right: 16px;
      gap: 8px;
      flex-wrap: wrap;
      justify-content: flex-end;
      max-width: calc(100% - 32px);
    }
    .album-card { padding: 16px; }
    .album-title { font-size: 1rem; }
  }
</style>
