<script lang="ts">
  export let items = [
    {
      title: 'Último Lanzamiento',
      text:
        'Descubre el nuevo single y guarda el track en tu biblioteca. Disponible en Spotify y YouTube.'
    },
    {
      title: 'Próximos Shows',
      text:
        'Entérate de fechas, ciudades y preventas. Únete a la lista para recibir avisos anticipados.'
    },
    {
      title: 'Comunidad',
      text:
        'Súmate al newsletter y sé parte del club de fans: sorteos, merch y contenido detrás de cámaras.'
    }
  ];
</script>

<section class="features">
  {#each items as it}
    <article class="item">
      <h4>{it.title}</h4>
      <p>{it.text}</p>
    </article>
  {/each}
</section>

<style>
  .features {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 28px;
    margin-top: 16px;
  }
  .item h4 {
    margin: 0 0 6px;
    font: 700 14px/1.1 Inter, system-ui, sans-serif;
    color: #3a3a3a;
  }
  .item p {
    margin: 0;
    font: 500 13px/1.5 Inter, system-ui, sans-serif;
    color: #6a6a6a;
  }
  @media (max-width: 860px) {
    .features { grid-template-columns: 1fr; }
  }
</style>
