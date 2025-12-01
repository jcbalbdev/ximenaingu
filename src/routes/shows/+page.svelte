<script lang="ts">
  import bgImage from '$lib/images/florayfaunaFINAL.jpg';
  import posterImage from '$lib/images/ximenaflorayfauna.png';

  // Datos del show
  const showTitle = "Un Ecosistema de Emociones Tour";
  const showSubtitle = "Vive una noche mágica con Ximena Ingü. Una experiencia íntima donde cada canción cobra vida.";
  const showDate = "15 de Febrero, 2025";
  const showTime = "8:00 PM";
  const showLocation = "Centro Cultural Lima, Lima - Perú";

  // Ejemplo: luego este botón redirige a otra sección interna
  const whatsappLink = "#entradas"; 
</script>

<!-- PAGE WRAPPER -->
<section class="relative w-full min-h-screen text-white overflow-hidden">

  <!-- BACKGROUND -->
  <div class="absolute inset-0">
    <img
      src={bgImage}
      alt="Fondo show"
      class="w-full h-full object-cover"
    />

    <!-- OVERLAY oscuro -->
    <div class="absolute inset-0 bg-black/60 backdrop-blur-md"></div>
  </div>

  <!-- CONTENT GRID -->
  <div class="relative z-10 max-w-7xl mx-auto px-6 py-24 grid grid-cols-1 lg:grid-cols-2 gap-14">

    <!-- LEFT CONTENT -->
    <div class="flex flex-col justify-center">

      <!-- PILL -->
      <span class="inline-block bg-orange-500 text-white font-semibold px-5 py-2 rounded-full mb-6 text-sm shadow-lg">
        Próximo Show
      </span>

      <!-- TITLE -->
      <h1 class="text-5xl lg:text-6xl font-extrabold leading-tight drop-shadow-xl">
        {showTitle}
      </h1>

      <!-- SUBTITLE -->
      <p class="text-gray-200 text-lg mt-6 max-w-xl">
        {showSubtitle}
      </p>

      <!-- INFO LIST -->
      <div class="mt-10 space-y-4 text-lg">

        <!-- Fecha -->
        <div class="flex items-center gap-3">
          <!-- ICON calendar -->
          <svg class="w-6 h-6 text-orange-400" fill="none" stroke="currentColor" stroke-width="2"
               viewBox="0 0 24 24" stroke-linecap="round" stroke-linejoin="round">
            <path d="M8 2v2m8-2v2m-9 4h10M5 22h14a2 2 0 0 0 2-2V8a2 2 0 0 0-2-2H5a2 2 0 0 0-2 2v12a2 2 0 0 0 2 2z"/>
          </svg>
          {showDate}
        </div>

        <!-- Hora -->
        <div class="flex items-center gap-3">
          <!-- ICON clock -->
          <svg class="w-6 h-6 text-orange-400" fill="none" stroke="currentColor" stroke-width="2"
               viewBox="0 0 24 24" stroke-linecap="round" stroke-linejoin="round">
            <path d="M12 6v6l3 3m6-3a9 9 0 1 1-18 0 9 9 0 0 1 18 0z"/>
          </svg>
          {showTime}
        </div>

        <!-- Ubicación -->
        <div class="flex items-center gap-3">
          <!-- ICON location -->
          <svg class="w-6 h-6 text-orange-400" fill="none" stroke="currentColor" stroke-width="2"
               viewBox="0 0 24 24" stroke-linecap="round" stroke-linejoin="round">
            <path d="M21 10c0 6-9 13-9 13S3 16 3 10a9 9 0 0 1 18 0z"/>
            <circle cx="12" cy="10" r="3"/>
          </svg>
          {showLocation}
        </div>

      </div>

      <!-- BUTTON -->
      <a
        href={whatsappLink}
        class="mt-10 inline-flex items-center gap-3 bg-green-500 hover:bg-green-600 text-black font-semibold px-6 py-3 rounded-full text-lg shadow-lg transition"
      >
        <!-- WhatsApp icon -->
        <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 24 24">
          <path d="M..."/>
        </svg>
        Comprar Entradas
      </a>
    </div>

    <!-- RIGHT POSTER IMAGE -->
    <div class="flex justify-center lg:justify-end">
      <img
        src={posterImage}
        alt="Poster del show"
        class="w-[80%] lg:w-[70%] rounded-3xl shadow-2xl object-cover"
      />
    </div>

  </div>

</section>

<!-- SECCIÓN: TIPOS DE ENTRADA -->
<section id="entradas" class="max-w-7xl mx-auto px-6 py-24 text-white">

  <!-- HEADER -->
  <div class="bg-black/70 backdrop-blur-xl border border-white/10 rounded-3xl px-10 py-10 text-center mb-16">
    <h2 class="text-4xl font-extrabold mb-4">Tipos de Entrada</h2>
    <p class="text-gray-300 max-w-2xl mx-auto text-lg">
      Elige tu entrada y cierra la compra directamente por WhatsApp. Pago seguro y confirmación inmediata.
    </p>
  </div>

  <!-- GRID DE TARJETAS -->
  <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-10">

    <!-- CARD 1: GENERAL -->
    <div class="bg-black/80 border border-white/10 rounded-3xl p-8 shadow-xl flex flex-col justify-between">
      
      <!-- ÍCONO -->
      <div class="text-orange-500 text-3xl mb-4">🎟</div>

      <h3 class="text-2xl font-bold">General</h3>
      <p class="text-4xl font-extrabold mt-2">S/ 80</p>

      <!-- BENEFICIOS -->
      <ul class="mt-6 space-y-3 text-gray-300">
        <li class="flex items-center gap-2">
          <svg class="w-5 h-5 text-gray-400" fill="none" stroke="currentColor" stroke-width="2"
               viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round"
               d="M5 13l4 4L19 7"/></svg>
          Acceso al evento
        </li>
        <li class="flex items-center gap-2">
          <svg class="w-5 h-5 text-gray-400" fill="none" stroke="currentColor" stroke-width="2"
               viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round"
               d="M5 13l4 4L19 7"/></svg>
          Zona general
        </li>
      </ul>

      <!-- BOTÓN -->
      <a href="#entradas"
         class="mt-8 w-full bg-white text-black font-semibold text-lg rounded-full py-3 text-center hover:bg-gray-200 transition">
        Comprar
      </a>

    </div>


    <!-- CARD 2: VIP (Destacado) -->
    <div class="bg-white text-black border-2 border-orange-500 rounded-3xl p-8 shadow-xl relative flex flex-col justify-between">

      <!-- BADGE SUPERIOR -->
      <span class="absolute -top-4 left-1/2 -translate-x-1/2 bg-orange-500 text-white px-4 py-1 rounded-full text-sm font-bold shadow-md">
        Más Popular
      </span>

      <!-- ÍCONO -->
      <div class="text-orange-500 text-3xl mb-4">⭐</div>

      <h3 class="text-2xl font-bold">VIP</h3>
      <p class="text-4xl font-extrabold mt-2">S/ 150</p>

      <!-- BENEFICIOS -->
      <ul class="mt-6 space-y-3 text-gray-700">
        <li class="flex items-center gap-2">
          <svg class="w-5 h-5 text-orange-500" fill="none" stroke="currentColor" stroke-width="2"
               viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round"
               d="M5 13l4 4L19 7"/></svg>
          Acceso al evento
        </li>
        <li class="flex items-center gap-2">
          <svg class="w-5 h-5 text-orange-500" fill="none" stroke="currentColor" stroke-width="2"
               viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round"
               d="M5 13l4 4L19 7"/></svg>
          Zona preferencial
        </li>
        <li class="flex items-center gap-2">
          <svg class="w-5 h-5 text-orange-500" fill="none" stroke="currentColor" stroke-width="2"
               viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round"
               d="M5 13l4 4L19 7"/></svg>
          Meet & Greet
        </li>
      </ul>

      <!-- BOTÓN -->
      <a href="#entradas"
         class="mt-8 w-full bg-black text-white font-semibold text-lg rounded-full py-3 text-center hover:bg-black/80 transition">
        Comprar
      </a>

    </div>


    <!-- CARD 3: GRUPO -->
    <div class="bg-black/80 border border-white/10 rounded-3xl p-8 shadow-xl flex flex-col justify-between">

      <!-- ÍCONO -->
      <div class="text-orange-500 text-3xl mb-4">👥</div>

      <h3 class="text-2xl font-bold">Grupo (4 personas)</h3>
      <p class="text-4xl font-extrabold mt-2">S/ 280</p>

      <!-- BENEFICIOS -->
      <ul class="mt-6 space-y-3 text-gray-300">
        <li class="flex items-center gap-2">
          <svg class="w-5 h-5 text-gray-400" fill="none" stroke="currentColor" stroke-width="2"
               viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round"
               d="M5 13l4 4L19 7"/></svg>
          4 entradas generales
        </li>
        <li class="flex items-center gap-2">
          <svg class="w-5 h-5 text-gray-400" fill="none" stroke="currentColor" stroke-width="2"
               viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round"
               d="M5 13l4 4L19 7"/></svg>
          Ahorra S/ 40
        </li>
      </ul>

      <!-- BOTÓN -->
      <a href="#entradas"
         class="mt-8 w-full bg-white text-black font-semibold text-lg rounded-full py-3 text-center hover:bg-gray-200 transition">
        Comprar
      </a>

    </div>

  </div>

</section>

