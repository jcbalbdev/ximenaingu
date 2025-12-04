<script lang="ts">
  // Luego puedes manejar el formulario con actions o un endpoint
</script>

<section class="max-w-6xl mx-auto px-6 py-20 text-white ">

  <!-- HEADER -->
  <div class="bg-black/60 backdrop-blur-xl  rounded-3xl px-10 py-10 text-center mb-16">
    <h1 class="text-4xl font-extrabold mb-4">Contacto</h1>
    <p class="text-gray-300 max-w-2xl mx-auto text-lg">
      ¿Eres una productora musical, sello discográfico o promotor de eventos? Conecta con el equipo de Ximena Ingü.
    </p>
  </div>


  <!-- GRID PRINCIPAL -->
  <div class="grid grid-cols-1 lg:grid-cols-3 gap-10">

    <!-- FORMULARIO -->
    <div class="lg:col-span-2 bg-black/60  rounded-3xl p-8 shadow-xl">

      <form class="space-y-6">

        <!-- Nombre / Empresa -->
        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
          <div>
            <label class="block font-semibold mb-2">Nombre completo *</label>
            <input
              type="text"
              placeholder="Tu nombre"
              class="w-full px-4 py-3 bg-black/40 border border-white/20 rounded-xl text-white placeholder-gray-400 outline-none focus:border-white"
            />
          </div>

          <div>
            <label class="block font-semibold mb-2">Empresa / Sello</label>
            <input
              type="text"
              placeholder="Nombre de tu empresa"
              class="w-full px-4 py-3 bg-black/40 border border-white/20 rounded-xl text-white placeholder-gray-400 outline-none focus:border-white"
            />
          </div>
        </div>

        <!-- Email -->
        <div>
          <label class="block font-semibold mb-2">Correo electrónico *</label>
          <input
            type="email"
            placeholder="correo@ejemplo.com"
            class="w-full px-4 py-3 bg-black/40 border border-white/20 rounded-xl text-white placeholder-gray-400 outline-none focus:border-white"
          />
        </div>

        <!-- Teléfono -->
        <div>
          <label class="block font-semibold mb-2">Teléfono</label>
          <input
            type="text"
            placeholder="+51 999 999 999"
            class="w-full px-4 py-3 bg-black/40 border border-white/20 rounded-xl text-white placeholder-gray-400 outline-none focus:border-white"
          />
        </div>

        <!-- Tipo de consulta -->
        <div>
          <label class="block font-semibold mb-2">Tipo de consulta *</label>
          <select
            class="w-full px-4 py-3 bg-black/40 border border-white/20 rounded-xl text-white outline-none focus:border-white"
          >
            <option disabled selected>Selecciona una opción</option>
            <option>Booking / Eventos</option>
            <option>Prensa / Medios</option>
            <option>Colaboraciones</option>
            <option>Otros</option>
          </select>
        </div>

        <!-- Mensaje -->
        <div>
          <label class="block font-semibold mb-2">Mensaje *</label>
          <textarea
            rows="4"
            placeholder="Cuéntanos sobre tu propuesta..."
            class="w-full px-4 py-3 bg-black/40 border border-white/20 rounded-xl text-white placeholder-gray-400 outline-none focus:border-white"
          ></textarea>
        </div>

        <!-- BOTÓN -->
        <button
          type="submit"
          class="mt-4 w-full bg-black/60 text-white font-semibold py-3 rounded-full text-lg hover:bg-[#121212] transition flex items-center justify-center gap-2"
        >
          <svg class="w-5 h-5" fill="none" stroke="currentColor" stroke-width="2"
               viewBox="0 0 24 24" stroke-linecap="round" stroke-linejoin="round">
            <path d="M22 2 11 13"></path>
            <path d="M22 2 15 22 11 13 2 9l20-7z"></path>
          </svg>
          Enviar Mensaje
        </button>

      </form>

    </div>


    <!-- COLUMNA DERECHA -->
    <div class="flex flex-col gap-10">

      <!-- MANAGEMENT & BOOKING -->
      <div class="bg-black/60 border border-white/10 rounded-3xl p-8 shadow-xl">
        <h3 class="text-2xl font-bold mb-4">Para Management y Booking</h3>

        <p class="text-gray-300">
          Si representas a una productora, festival o venue y deseas incluir a Ximena Ingü en tu evento, contacta directamente a nuestro equipo.
        </p>

        <div class="mt-6 flex items-center gap-3 text-orange-400 font-semibold break-all">
          <svg class="w-6 h-6" fill="none" stroke="currentColor" stroke-width="2"
               viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round"
                  d="M4 4h16v16H4z"></path>
            <path stroke-linecap="round" stroke-linejoin="round"
                  d="m22 4-10 9L2 4"></path>
          </svg>
          management@ximenaingu.com
        </div>
      </div>

      <!-- REDES SOCIALES -->
      <div class="bg-black/60 border border-white/10 rounded-3xl p-8 shadow-xl">
        <h3 class="text-2xl font-bold mb-6">Redes Sociales</h3>

        <div class="space-y-5 text-gray-300">

          <!-- Instagram -->
          <div class="flex items-center gap-4">
            <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" stroke-width="2"
                 viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round"
                    d="M7 2h10a5 5 0 0 1 5 5v10a5 5 0 0 1-5 5H7a5 5 0 0 1-5-5V7a5 5 0 0 1 5-5z" />
              <circle cx="12" cy="12" r="3.5" />
            </svg>

            <div>
              <p class="font-semibold">Instagram</p>
              <p class="text-sm">@ximenaingu</p>
            </div>
          </div>

          <!-- Spotify -->
          <div class="flex items-center gap-4">
            <svg class="w-6 h-6 text-white" fill="currentColor" viewBox="0 0 24 24">
              <path d="M12 0a12 12 0 1 0 12 12A12.035 12.035 0 0 0 12 0Zm5.19 17.32a.78.78 0 0 1-1.08.26c-2.95-1.8-6.66-2.21-11.05-1.2a.78.78 0 1 1-.34-1.52c4.82-1.09 9.01-.62 12.37 1.39a.78.78 0 0 1 .1 1.07Zm1.52-3c-.23.36-.69.47-1.05.25-3.38-2.09-8.53-2.7-12.53-1.47a.78.78 0 0 1-.46-1.5c4.41-1.32 10.07-.63 13.88 1.69a.78.78 0 0 1 .16 1.03Zm.12-3.22a.78.78 0 0 1-1.09.17c-3.89-2.37-10.85-2.58-14.76-1.38a.78.78 0 1 1-.46-1.49c4.37-1.36 12.06-1.12 16.48 1.57a.78.78 0 0 1 .17 1.13Z" />
            </svg>

            <div>
              <p class="font-semibold">Spotify</p>
              <p class="text-sm">Ximena Ingü</p>
            </div>
          </div>

          <!-- YouTube -->
          <div class="flex items-center gap-4">
            <svg class="w-6 h-6 text-white" fill="currentColor" viewBox="0 0 24 24">
              <path
                d="M22.54 6.42a2.78 2.78 0 0 0-1.95-2C18.64 4 12 4 12 4s-6.64 0-8.59.46a2.78 2.78 0 0 0-1.95 2A29.94 29.94 0 0 0 1 12a29.94 29.94 0 0 0 .46 5.58 2.78 2.78 0 0 0 1.95 2C5.36 20 12 20 12 20s6.64 0 8.59-.46a2.78 2.78 0 0 0 1.95-2A29.94 29.94 0 0 0 23 12a29.94 29.94 0 0 0-.46-5.58ZM10 15.46V8.54L15.82 12Z"
              />
            </svg>

            <div>
              <p class="font-semibold">YouTube</p>
              <p class="text-sm">Ximena Ingü</p>
            </div>
          </div>

        </div>
      </div>

    </div>

  </div>

</section>
