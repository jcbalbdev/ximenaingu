<script>
  import { onMount } from "svelte";
import flora from '$lib/images/florayfaunaFINAL.jpg';
  import tren from '$lib/images/eltren.png';
  import desaparecer from '$lib/images/desaparecer.png';
  let search = "";
  let showAutocomplete = false;
  let selected = "Todas";

  let filters = ["Todas", "Spotify", "YouTube", "YouTube Music", "Apple Music"];

  let songs = [
    {
      title: "El Tren",
      album: "Flora y Fauna",
      image: tren,
      url: "https://open.spotify.com/track/xxxxx",
      platforms: ["spotify", "youtube"]
    },
    {
      title: "Flora y Fauna",
      album: "Flora y Fauna",
      image: flora,
      url: "https://open.spotify.com/track/xxxxx",
      platforms: ["spotify", "youtube"]
    },
    {
      title: "Des-aparecer",
      album: "Singles",
      image: desaparecer,
      url: "https://open.spotify.com/track/xxxxx",
      platforms: ["spotify"]
    },
    {
      title: "Despertar",
      album: "Singles",
      image: tren,
      url: "https://youtube.com/watch?v=xxxx",
      platforms: ["youtube"]
    },
    {
      title: "Raíces",
      album: "Flora y Fauna",
      image: flora,
      url: "https://open.spotify.com/track/xxxxx",
      platforms: ["spotify", "youtube"]
    },
    {
      title: "Cielo Abierto",
      album: "Singles",
      image: desaparecer,
      url: "https://youtube.com/watch?v=xxxx",
      platforms: ["youtube"]
    },
    {
      title: "Mariposa",
      album: "Flora y Fauna",
      image: flora,
      url: "https://open.spotify.com/track/xxxxx",
      platforms: ["spotify", "youtube"]
    },
    {
      title: "Silencio",
      album: "Singles",
      image: desaparecer,
      url: "https://open.spotify.com/track/xxxxx",
      platforms: ["spotify"]
    }
  ];

  /** FILTRO PRINCIPAL (buscador + plataforma) */
  $: filteredSongs =
    songs.filter((song) => {
      const textMatch =
        song.title.toLowerCase().includes(search.toLowerCase()) ||
        song.album.toLowerCase().includes(search.toLowerCase());

      const platformMatch =
        selected === "Todas" ||
        song.platforms.includes(selected.toLowerCase());

      return textMatch && platformMatch;
    });

  /** AUTOCOMPLETADO */
  $: suggestions =
    search.length > 0
      ? songs.filter((s) =>
          (s.title + " " + s.album)
            .toLowerCase()
            .includes(search.toLowerCase())
        )
      : [];
</script>

<div class="page-wrapper">

  <!-- HERO -->
  <section class="hero">
    <h1>Música</h1>
    <p>Explora todas las canciones de Ximena Ingü. Filtra por plataforma y encuentra tu próximo track favorito.</p>

    <!-- SEARCH WITH AUTOCOMPLETE -->
    <div class="search-wrapper">
      <input
        type="text"
        bind:value={search}
        placeholder="Buscar por canción o álbum…"
        on:input={() => (showAutocomplete = true)}
        on:focus={() => (showAutocomplete = true)}
      />

      {#if showAutocomplete && suggestions.length > 0}
        <div class="autocomplete">
          {#each suggestions as item}
            <div
              class="suggestion"
              on:click={() => {
                search = item.title;
                showAutocomplete = false;
              }}
            >
              {item.title} — <span>{item.album}</span>
            </div>
          {/each}
        </div>
      {/if}
    </div>

    <!-- PLATFORM FILTERS -->
    <div class="filters">
      {#each filters as f}
        <button
          class:selected={selected === f}
          on:click={() => (selected = f)}
        >
          {f}
        </button>
      {/each}
    </div>
  </section>

  <!-- GRID OF SONGS -->
  <section class="music-grid">
    {#each filteredSongs as song}
      <a class="song-card" href={song.url} target="_blank">

        <div class="image-wrapper">
          <img src={song.image} alt={song.title} />

          <button
            class="play-btn"
            on:click={(e) => {
              e.preventDefault();
              window.open(song.url, "_blank");
            }}
          >
            ▶
          </button>
        </div>

        <h3>{song.title}</h3>
        <p>{song.album}</p>
      </a>
    {/each}
  </section>

</div>

<style>
  .page-wrapper {
    padding: 60px 20px;
    max-width: 1400px;
    margin: 0 auto;
  }

  /* HERO BLOCK */
  .hero {
    padding: 40px;
    text-align: center;
    backdrop-filter: blur(18px);
    color:#fff;
    background: rgba(255, 255, 255, 0.2);
    border-radius: 22px;
    margin-bottom: 50px;
  }

  .search-wrapper {
    position: relative;
    max-width: 600px;
    margin: 24px auto 0;
  }

  .search-wrapper input {
    width: 100%;
    padding: 14px 18px;
    border-radius: 20px;
    background: rgba(0, 0, 0, 0.5);
    color: white;
    border: none;
  }

  /* AUTOCOMPLETE */
  .autocomplete {
    position: absolute;
    top: 50px;
    left: 0;
    width: 100%;
    color:#fff;
    background: rgba(0, 0, 0, 0.5);
    border-radius: 14px;
    backdrop-filter: blur(14px);
    overflow: hidden;
    z-index: 0;
  }

  .suggestion {
    padding: 10px 15px;
    cursor: pointer;
    font-size: 0.95rem;
  }
  .suggestion:hover {
    background: #121212;
    border-radius: 14px;
  }
  .suggestion span {
    color: #fff;
  }

  /* PLATFORM FILTERS */
  .filters {
    margin-top: 16px;
    display: flex;
    gap: 12px;
    justify-content: center;
    flex-wrap: wrap;
  }

  .filters button {
    padding: 6px 16px;
    border-radius: 16px;
    border: none;
    background: rgba(0,0,0,0.5);
    color: white;
    cursor: pointer;
    transition: 0.2s;
  }

  .filters button.selected {
    background: white;
    color: black;
  }

  /* GRID */
  .music-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
    gap: 28px;
  }

  /* SONG CARD */
  .song-card {
    display: block;
    text-decoration: none;
    color: white;

    background: rgba(255, 255, 255, 0.06);
    border-radius: 14px;
    border: 1px solid rgba(255, 255, 255, 0.1);
    padding: 10px;
    transition: 0.25s;
  }

  .song-card:hover {
    background: rgba(255, 255, 255, 0.12);
    transform: translateY(-4px);
  }

  /* IMAGE + PLAY BUTTON */
  .image-wrapper {
    position: relative;
    border-radius: 14px;
    overflow: hidden;
  }

  .image-wrapper img {
    width: 100%;
    border-radius: 14px;
    object-fit: cover;
  }

  .play-btn {
    position: absolute;
    right: 10px;
    bottom: 10px;

    width: 48px;
    height: 48px;
    border-radius: 50%;
    background: #1db954;
    color: black;
    border: none;
    font-size: 20px;
    cursor: pointer;

    opacity: 0;
    transform: translateY(10px);
    transition: opacity 0.25s, transform 0.25s;
  }

  .image-wrapper:hover .play-btn {
    opacity: 1;
    transform: translateY(0);
  }

  h3 {
    margin: 12px 0 4px;
    font-size: 1rem;
  }

  p {
    margin: 0;
    color: #ccc;
  }
</style>
