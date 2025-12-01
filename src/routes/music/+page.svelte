<script>
  import flora from '$lib/images/florayfaunaFINAL.jpg';

  let search = "";
  let showAutocomplete = false;
  let selected = "Todas";

  let filters = ["Todas", "Spotify", "YouTube", "YouTube Music", "Apple Music"];

  let songs = [
    { title: "El Tren", album: "Flora y Fauna", image: flora, url: "https://open.spotify.com/intl-es/track/652oyyfPU6q9EWpteMoC7N", platforms: ["spotify","youtube"] },
    { title: "Flora y Fauna", album: "Flora y Fauna", image: flora, url: "https://open.spotify.com/intl-es/track/2iz3tJYDjq2qIqEiBHfVMG", platforms: ["spotify","youtube"] },
    { title: "Des-aparecer", album: "Flora y Fauna", image: flora, url: "https://open.spotify.com/intl-es/track/5MhnSbgrzSPVi3ZMxOFM17", platforms: ["spotify"] },
    { title: "Ser Uno Mismo", album: "Flora y Fauna", image: flora, url: "https://open.spotify.com/intl-es/track/2nVYGTJqDIWHMhZDsbjSXQ", platforms: ["spotify"] },
    { title: "Interludio Triste", album: "Flora y Fauna", image: flora, url: "https://open.spotify.com/intl-es/track/1xkNGkOlLVVtANbNIxdS22", platforms: ["spotify","youtube"] },
    { title: "A Salvo", album: "Flora y Fauna", image: flora, url: "https://open.spotify.com/intl-es/track/2hMgbgjVTz5hUJfLDAg6HB", platforms: ["youtube"] },
    { title: "Yo Te Vi En Mí", album: "Flora y Fauna", image: flora, url: "https://open.spotify.com/intl-es/track/4QNMWvsUFkaNmzj6C9VuPy", platforms: ["spotify","youtube"] },
    { title: "Florecer", album: "Flora y Fauna", image: flora, url: "https://open.spotify.com/intl-es/track/1fj9VVKXVOZYLQE9zoHHmu", platforms: ["spotify"] },
    { title: "Morirvivir", album: "Flora y Fauna", image: flora, url: "https://open.spotify.com/intl-es/track/25DVj6frMyw0Pui0sjiVcT", platforms: ["spotify"] }
  ];

  /** FILTERED LIST */
  $: filteredSongs = songs.filter(song => {
    const matchesText =
      song.title.toLowerCase().includes(search.toLowerCase()) ||
      song.album.toLowerCase().includes(search.toLowerCase());

    const matchesPlatform =
      selected === "Todas" || song.platforms.includes(selected.toLowerCase());

    return matchesText && matchesPlatform;
  });

  /** AUTOCOMPLETE */
  $: suggestions =
    search.length > 0
      ? songs.filter(s =>
          (s.title + " " + s.album)
            .toLowerCase()
            .includes(search.toLowerCase())
        )
      : [];
</script>


<!-- PAGE WRAPPER -->
<div class="max-w-[1400px] mx-auto px-6 py-12">

  <!-- HERO -->
  <section class="relative z-10 backdrop-blur-xl bg-white/20 p-10 rounded-3xl text-center  mb-12 text-white">

    <h1 class="text-5xl font-bold">Música</h1>
    <p class="text-gray-200 mt-3 max-w-2xl mx-auto">
      Explora todas las canciones de Ximena Ingü. Filtra por plataforma y encuentra tu próximo track favorito.
    </p>


    <!-- SEARCH WRAPPER -->
    <div class="relative mx-auto mt-8 max-w-lg z-[9999]">

      <!-- SEARCH BAR -->
      <div class="relative">

        <!-- SEARCH ICON -->
        <div class="absolute inset-y-0 left-0 flex items-center pl-4 pointer-events-none">
          <svg class="w-5 h-5 text-gray-200 opacity-90"
            xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
            stroke="currentColor" stroke-width="2">
            <path stroke-linecap="round" stroke-linejoin="round"
              d="m21 21-4.35-4.35m0 0A7.5 7.5 0 103.6 3.6a7.5 7.5 0 0013.05 13.05z" />
          </svg>
        </div>

        <!-- INPUT FIELD -->
        <input
          type="text"
          bind:value={search}
          placeholder="Buscar por canción o álbum…"
          class="
            block w-full py-3.5 pl-12 pr-10
            bg-black/40 border border-white/20
            text-white text-sm rounded-full
            placeholder:text-gray-300

            appearance-none focus:appearance-none
            outline-none focus:outline-none
            ring-0 focus:ring-0
            focus:border-white
            transition
          "
          on:input={() => (showAutocomplete = true)}
          on:focus={() => (showAutocomplete = true)}
        />

        <!-- CLEAR BUTTON -->
        {#if search.length > 0}
          <button
            type="button"
            on:click={() => { search = ""; showAutocomplete = false; }}
            class="absolute inset-y-0 right-0 flex items-center pr-4 text-gray-200 hover:text-white transition"
          >
            <svg class="w-5 h-5"
              xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
              stroke="currentColor" stroke-width="2">
              <path stroke-linecap="round" stroke-linejoin="round"
                d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>
        {/if}

      </div>

      <!-- AUTOCOMPLETE -->
      {#if showAutocomplete && suggestions.length > 0}
        <div
          class="absolute top-14 left-0 w-full bg-black/70 backdrop-blur-xl
                 border border-white/20 rounded-2xl shadow-2xl
                 max-h-64 overflow-y-auto z-[9999]"
        >
          {#each suggestions as item}
            <div
              class="flex items-center gap-4 px-4 py-3 hover:bg-[#121212] cursor-pointer transition"
              on:click={() => {
                search = item.title;
                showAutocomplete = false;
              }}
            >
              <img src={item.image} class="w-10 h-10 rounded-md object-cover" />
              <div>
                <p class="text-white text-sm font-medium">{item.title}</p>
                <p class="text-gray-400 text-xs">{item.album}</p>
              </div>
            </div>
          {/each}
        </div>
      {/if}

    </div>


    <!-- FILTERS -->
    <div class="flex flex-wrap justify-center gap-3 mt-6">
      {#each filters as f}
        <button
          on:click={() => (selected = f)}
          class={`px-5 py-2 rounded-2xl text-sm transition ${
            selected === f
              ? "bg-white text-black "
              : "bg-black/60 text-white hover:bg-[#121212] "
          }`}
        >
          {f}
        </button>
      {/each}
    </div>

  </section>

  <!-- SONG GRID -->
  <section class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 gap-8 text-white">
    {#each filteredSongs as song}
      <a href={song.url} target="_blank" class="group block hover:bg-black/20 p-3 rounded-2xl transition">

        <div class="relative rounded-2xl overflow-hidden">
          <img src={song.image} class="w-full h-full object-cover rounded-2xl" />

          <!-- PLAY BUTTON -->
          <button
            class="absolute bottom-3 right-3 w-12 h-12 rounded-full bg-green-500 text-black text-xl
                   flex items-center justify-center opacity-0 translate-y-3
                   group-hover:opacity-100 group-hover:translate-y-0 transition"
            on:click={(e) => {
              e.preventDefault();
              window.open(song.url, "_blank");
            }}
          >
            ▶
          </button>
        </div>

        <h3 class="font-semibold mt-3 text-white">{song.title}</h3>
        <p class="text-sm text-gray-300 -mt-1">{song.album}</p>

      </a>
    {/each}
  </section>

</div>

<style>
  /* Remove Chrome/Windows Input Highlight */
  input::-webkit-focus-inner {
    border: 0 !important;
    padding: 0 !important;
  }
</style>
