<script>
  import flora from '$lib/images/florayfaunaFINAL.jpg';
  import tren from '$lib/images/eltren.png';
  import desaparecer from '$lib/images/desaparecer.png';
  export let items = [
    {
      title: "Último Lanzamiento",
      description: 'Escucha mi álbum debut "Flora y Fauna" en todas las plataformas digitales.',
      image: flora
    },
    {
      title: "Próximos Shows",
      description: "Entérate de los próximos conciertos y eventos en los que puedes escuchar a Ximena en vivo.",
      image: tren
    },
    {
      title: "Comunidad",
      description: 'Únete a la "Comunidad Emocional"  en Whatsapp para recibir contenido exclusivo.',
      image: desaparecer
    }
  ];
</script>

<section class="feature-wrapper">
  <div class="feature-grid">
    {#each items as item}
      <div class="feature-card">
        <div class="image">
          <img src={item.image} alt={item.title} />
        </div>

        <div class="content">
          <h3>{item.title}</h3>
          <p>{item.description}</p>
        </div>
      </div>
    {/each}
  </div>
</section>

<style>
  .feature-wrapper {
    padding: 40px 20px 20px;
    max-width: 1200px;
    margin: 0 auto;
  }

  .feature-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 24px;
  }

  .feature-card {
    background: rgba(255, 255, 255, 0.03);
    border: 1px solid rgba(255, 255, 255, 0.08);
    border-radius: 18px;
    overflow: hidden;
    backdrop-filter: blur(4px);
    transition: transform 0.25s ease, opacity 0.25s ease;
  }

  .feature-card:hover {
    transform: translateY(-4px);
    opacity: 0.95;
  }

  .image img {
    width: 100%;
    height: 170px;
    object-fit: cover;
  }

  .content {
    padding: 16px 20px 20px;
    background: rgba(0, 0, 0, 0.2);
  }

  .content h3 {
    margin: 0 0 10px;
    font-size: 1.1rem;
    font-weight: 700;
    color: #fff;
  }

  .content p {
    margin: 0;
    font-size: 0.95rem;
    line-height: 1.4;
    color: #fff;
  }

  /* Responsive */
  @media (max-width: 900px) {
    .feature-grid {
      grid-template-columns: 1fr;
      gap: 18px;
    }

    .image img {
      height: 150px;
    }
  }
</style>
