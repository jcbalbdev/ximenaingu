<script lang="ts">
  import spotifyicon from '$lib/images/Spotify-Icon-Black-Logo.svg';
  // Header simple y accesible para SvelteKit
  import { page } from '$app/stores';

  export let artistName = 'Ximena Ingü';
  export let spotifyUrl = 'https://open.spotify.com/intl-es/artist/4iF5aAIAVZQKagPignOUNO';

  // enlaces principales de la landing
  const links = [
    { href: '/', label: 'Inicio' },
    { href: '/about', label: 'Sobre mí' },
    { href: '/music', label: 'Música' },
    { href: '/shows', label: 'Shows' },
    { href: '/contact', label: 'Contacto' }
  ];

  let mobileOpen = false;

  // resalta la ruta actual
  $: activePath = $page.url.pathname.replace(/\/+$/, '') || '/';
  const isActive = (href: string) =>
    (href === '/' ? activePath === '/' : activePath.startsWith(href));
</script>

<header class="site-header">
  <nav class="container">
    <!-- Branding -->
    <a class="brand" href="/" aria-label="Ir a inicio">
      <span class="brand__name">{artistName}</span>
    </a>

    <!-- Navegación (desktop) -->
    <ul class="nav">
      {#each links as link}
        <li>
          <a
            href={link.href}
            class:active={isActive(link.href)}
            aria-current={isActive(link.href) ? 'page' : undefined}
            >{link.label}</a
          >
        </li>
      {/each}
    </ul>

    <!-- CTA Spotify (desktop) -->
    <a
  class="spotify-cta"
  href={spotifyUrl}
  target="_blank"
  rel="noopener noreferrer"
>
  <img
    src={spotifyicon}
    alt="Spotify logo"
    class="spotify-cta__icon"
  />
  Escuchar en Spotify
</a>

    <!-- Toggle móvil -->
    <button
      class="menu-btn"
      aria-label="Abrir menú"
      aria-expanded={mobileOpen}
      on:click={() => (mobileOpen = !mobileOpen)}>
      <span class="menu-btn__bar" />
      <span class="menu-btn__bar" />
      <span class="menu-btn__bar" />
    </button>
  </nav>

  <!-- Menú móvil -->
  {#if mobileOpen}
    <div class="mobile-sheet" role="dialog" aria-label="Navegación móvil">
      <ul>
        {#each links as link}
          <li>
            <a
              href={link.href}
              class:active={isActive(link.href)}
              on:click={() => (mobileOpen = false)}>{link.label}</a>
          </li>
        {/each}
        <li class="mobile-cta">
          <a href={spotifyUrl} target="_blank" rel="noopener">Escuchar en Spotify</a>
        </li>
      </ul>
    </div>
  {/if}
</header>

<style>
  :global(body) {
    margin: 0;
  }

  .site-header {
    position: sticky;
    top: 0;
    z-index: 50;
    background: rgba(0, 0, 0, 0.5);
    backdrop-filter: saturate(1.1) blur(6px);
    border-bottom: 1px solid #121212;
  }

  .container {
    max-width: 89rem;
    margin: 0 auto;
    padding: 12px 16px;
    display: grid;
    grid-template-columns: auto 1fr auto auto;
    gap: 12px;
    align-items: center;
  }

  .brand {
    display: inline-flex;
    gap: 10px;
    align-items: center;
    text-decoration: none;
  }

  .brand__name {
    font: 600 16px/1.1 system-ui, -apple-system, Segoe UI, Roboto, Inter, "Helvetica Neue", Arial, sans-serif;
    color: #fff;
    letter-spacing: 0.2px;
  }

  .nav {
    list-style: none;
    display: flex;
    gap: 18px;
    margin: 0;
    padding: 0 8px;
    justify-self: center;
  }
  .nav a {
    text-decoration: none;
    color: #444;
    font: 500 14px/1.2 system-ui, -apple-system, Segoe UI, Roboto, Inter, "Helvetica Neue", Arial, sans-serif;
    padding: 6px 2px;
    border-bottom: 2px solid transparent;
  }
  .nav a:hover { color: #fff; }
  .nav a.active {
    color: #fff;
    border-color: #fff;
  }

  .spotify-cta {
    justify-self: end;
    text-decoration: none;
    display: inline-flex;
    align-items: center;
    gap: 8px;
    padding: 10px 14px;
    border-radius: 10px;
    border: 1px solid #111;
    color: #111;
    font: 600 14px/1 system-ui, -apple-system, Segoe UI, Roboto, Inter, "Helvetica Neue", Arial, sans-serif;
  }
  .spotify-cta__icon {
    width: 1.2rem;
    height: 1.2rem;
    fill: currentColor;
  }

  .menu-btn {
    display: none;
    width: 40px;
    height: 40px;
    padding: 0;
    border: 1px solid #ddd;
    border-radius: 10px;
    background: #fff;
  }
  .menu-btn__bar {
    display: block;
    width: 20px;
    height: 2px;
    margin: 4px auto;
    background: #111;
  }

  /* Móvil */
  @media (max-width: 860px) {
    .container {
      grid-template-columns: auto 1fr auto;
    }

    .nav,
    .spotify-cta {
      display: none;
    }

    .menu-btn {
      display: inline-block;
      justify-self: end;
    }

    .mobile-sheet {
      border-top: 1px solid #eee;
      background: #fff;
      padding: 8px 16px 16px;
    }
    .mobile-sheet ul {
      list-style: none;
      margin: 0;
      padding: 8px 0 0;
      display: grid;
      gap: 8px;
    }
    .mobile-sheet a {
      display: block;
      padding: 12px 4px;
      text-decoration: none;
      color: #222;
      border-radius: 8px;
    }
    .mobile-sheet a.active {
      background: #f4f4f4;
    }
    .mobile-cta a {
      text-align: center;
      border: 1px solid #111;
      border-radius: 10px;
    }
  }
</style>

