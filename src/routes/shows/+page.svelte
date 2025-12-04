<script lang="ts">
  
  import heroBg from '$lib/images/ximenaFlyerhor.jpg';
  
  import eventImg from '$lib/images/florayfaunaFINAL.jpg';
  import logo from '$lib/images/logoIngu.png';
  
  import { onMount } from 'svelte';
  // Fecha del concierto
  const endDate = new Date("2026-01-15T20:00:00");

  // Split-flap values
  let days = "00";
  let hours = "00";
  let minutes = "00";
  let seconds = "00";

  // Valores previos (para animación)
  let prevDays = "00";
  let prevHours = "00";
  let prevMinutes = "00";
  let prevSeconds = "00";

  // Actualiza contador
  function updateCountdown() {
    const now = Date.now();
    const diff = endDate.getTime() - now;

    if (diff <= 0) return;

    const d = Math.floor(diff / (1000 * 60 * 60 * 24));
    const h = Math.floor((diff / (1000 * 60 * 60)) % 24);
    const m = Math.floor((diff / (1000 * 60)) % 60);
    const s = Math.floor((diff / 1000) % 60);

    prevDays = days;
    prevHours = hours;
    prevMinutes = minutes;
    prevSeconds = seconds;

    days = String(d).padStart(2, "0");
    hours = String(h).padStart(2, "0");
    minutes = String(m).padStart(2, "0");
    seconds = String(s).padStart(2, "0");

    triggerFlap("days", prevDays, days);
    triggerFlap("hours", prevHours, hours);
    triggerFlap("minutes", prevMinutes, minutes);
    triggerFlap("seconds", prevSeconds, seconds);
  }

  // Aplica animación split-flap
  function triggerFlap(id: string, prevVal: string, newVal: string) {
    if (prevVal === newVal) return;

    const container = document.getElementById(`split-${id}`);
    if (!container) return;

    const digits = container.querySelectorAll(".split-flap-digit");

    digits.forEach((digit, index) => {
      const prevDigit = prevVal[index];
      const newDigit = newVal[index];

      if (prevDigit === newDigit) return;

      const top = digit.querySelector(".top");
      const bottom = digit.querySelector(".bottom");

      digit.setAttribute("data-prev", prevDigit);
      digit.setAttribute("data-now", newDigit);

      // Animar
      top.classList.add("animated", "final");
      bottom.classList.add("animated", "final");

      // Reset después
      setTimeout(() => {
        top.classList.remove("animated", "final");
        bottom.classList.remove("animated", "final");
      }, 350);
    });
  }

  // Start countdown
  onMount(() => {
    updateCountdown();
    const i = setInterval(updateCountdown, 1000);
    return () => clearInterval(i);
  });

  // PRECIOS
  const precioPreventa = 35;
  const promoPreventaTotal = 70; // 2x70

  const precioGeneral = 40;

  // Estado para ticket general
  let cantidadGeneral = 1;

  // Enviar WhatsApp
  function comprarPreventa() {
    const mensaje = encodeURIComponent(
      `Hola, quisiera comprar la PROMOCION  para el concierto "Flora y Fauna en el teatro".\nPromo: 2x70\nTotal: S/ ${promoPreventaTotal}`
    );
    window.open(`https://wa.me/51949201141?text=${mensaje}`, "_blank");
  }

  function comprarGeneral() {
    const total = precioGeneral * cantidadGeneral;
    const mensaje = encodeURIComponent(
      `Hola, quisiera comprar la ENTRADA GENERAL para el concierto "Flora y Fauna en el teatro".\nCantidad: ${cantidadGeneral}\nTotal: S/ ${total}`
    );
    window.open(`https://wa.me/51949201141?text=${mensaje}`, "_blank");
  }
</script>

<!-- ============================================= -->
<!--                   BANNER                     -->
<!-- ============================================= -->

<section class="relative w-full rounded-t-2xl overflow-hidden">

  <img 
    src={heroBg}
    alt="Banner Preventa"
    class="w-full h-auto object-contain mx-auto"
  />

  <!-- TEXTO SOBRE IMAGEN -->
  <div class="absolute inset-0 flex flex-col justify-center items-center text-white px-6 bg-black/40">

  </div>

</section>


<!-- ============================================= -->
<!--                 COUNTDOWN SPLIT-FLAP          -->
<!-- ============================================= -->

<section class="bg-black/60 py-20 text-center text-white">

  <h3 class="text-3xl font-extrabold tracking-wide mb-10">
    EL CONCIERTO LLEGA EN:
  </h3>

  <div class="split-flap-display">

    <!-- DÍAS -->
    <div id="split-days" class="flex gap-2">
      {#each days.split('') as d}
        <div class="split-flap-digit" data-prev={d} data-now={d}>
          <div class="split-flap-part top">
            <span>{d}</span>
          </div>
          <div class="split-flap-hinge"></div>
          <div class="split-flap-part bottom">
            <span>{d}</span>
          </div>
        </div>
      {/each}
    </div>

    <span class="text-5xl font-extrabold">:</span>

    <!-- HORAS -->
    <div id="split-hours" class="flex gap-2">
      {#each hours.split('') as d}
        <div class="split-flap-digit" data-prev={d} data-now={d}>
          <div class="split-flap-part top">
            <span>{d}</span>
          </div>
          <div class="split-flap-hinge"></div>
          <div class="split-flap-part bottom">
            <span>{d}</span>
          </div>
        </div>
      {/each}
    </div>

    <span class="text-5xl font-extrabold">:</span>

    <!-- MINUTOS -->
    <div id="split-minutes" class="flex gap-2">
      {#each minutes.split('') as d}
        <div class="split-flap-digit" data-prev={d} data-now={d}>
          <div class="split-flap-part top">
            <span>{d}</span>
          </div>
          <div class="split-flap-hinge"></div>
          <div class="split-flap-part bottom">
            <span>{d}</span>
          </div>
        </div>
      {/each}
    </div>

    <span class="text-5xl font-extrabold">:</span>

    <!-- SEGUNDOS -->
    <div id="split-seconds" class="flex gap-2">
      {#each seconds.split('') as d}
        <div class="split-flap-digit" data-prev={d} data-now={d}>
          <div class="split-flap-part top">
            <span>{d}</span>
          </div>
          <div class="split-flap-hinge"></div>
          <div class="split-flap-part bottom">
            <span>{d}</span>
          </div>
        </div>
      {/each}
    </div>

  </div>
<button
  on:click={() => {
    const section = document.getElementById("entradas");
    if (section) section.scrollIntoView({ behavior: "smooth" });
  }}
  class="mt-10 bg-yellow-400 hover:bg-yellow-300 text-black font-bold py-3 px-6 rounded-xl transition"
>
  Comprar Entradas
</button>
</section>




<!-- ============================================= -->
<!--              ¿CÓMO COMPRAR?                  -->
<!-- ============================================= -->

<section id="como-comprar" class="bg-black/60 text-white py-20 px-6 text-center">

  <h1 class="text-xl font-extrabold mb-4">
    ¿CÓMO <span class="text-red-500">COMPRAR</span> TU ENTRADA?
  </h1>

  <p class="text-gray-300 max-w-2xl mx-auto mb-12">
    Realiza tu compra de forma rápida y segura. Solo sigue estos simples pasos:
  </p>

  <div class="grid grid-cols-1 md:grid-cols-3 gap-10 max-w-6xl mx-auto">


    <!-- PASO 1 -->
    <div class="glass p-10 rounded-2xl shadow-xl border border-white/10">
      <h3 class="text-red-500 font-bold mb-2">PASO 1</h3>
      <h4 class="font-bold text-2xl mb-4">Elige tu tipo de entrada</h4>

      <p class="text-gray-300 leading-relaxed">
        Selecciona entre <span class="font-bold text-white">Preventa</span>  
        (S/35 o promo 2x70) o <span class="font-bold text-white">General</span>
        (1, 2 o 3 entradas).
      </p>
    </div>


    <!-- PASO 2 -->
    <div class="glass p-10 rounded-2xl shadow-xl border border-white/10">
      <h3 class="text-red-500 font-bold mb-2">PASO 2</h3>
      <h4 class="font-bold text-2xl mb-4">Haz clic en “Comprar”</h4>

      <p class="text-gray-300 leading-relaxed">
        El sistema abrirá automáticamente  
        <span class="font-bold text-white">WhatsApp</span>  
        con un mensaje prellenado indicando:
        <br />– Tipo de entrada  
        <br />– Cantidad  
        <br />– Total a pagar  
      </p>
    </div>


    <!-- PASO 3 -->
    <div class="glass p-10 rounded-2xl shadow-xl border border-white/10">
      <h3 class="text-red-500 font-bold mb-2">PASO 3</h3>
      <h4 class="font-bold text-2xl mb-4">Finaliza tu compra</h4>

      <p class="text-gray-300 leading-relaxed">
        Nuestro equipo te responderá por WhatsApp  
        para confirmar tu compra.  
        Luego recibirás tu <span class="font-bold text-white">entrada digital</span>  
        directamente en tu celular.
      </p>
    </div>

  </div>

</section>


<!-- ============================================= -->
<!--             SECCIÓN TICKETS (GLASS)          -->
<!-- ============================================= -->

<section id="entradas" class="py-20 px-6 bg-black/60 text-white">

  <h1 class="text-center text-4xl font-extrabold mb-3 tracking-tight">
    TICKETS <span class="text-yellow-400">FLORA & FAUNA</span>
  </h1>

  <p class="text-center text-gray-300 mb-14">
    Selecciona tu tipo de entrada favorito.
  </p>

  <!-- GRID -->
  <div class="grid grid-cols-1 md:grid-cols-2 gap-10 max-w-5xl mx-auto">

    <!-- ========================= -->
    <!--      TICKET PREVENTA      -->
    <!-- ========================= -->
    <div class="border-2 border-yellow-400 p-8 rounded-2xl bg-[#121212] text-center shadow-2xl">

      <h3 class="text-2xl font-bold text-yellow-400 mb-2 uppercase tracking-wide">
        Promocion
      </h3>

      <p class="text-gray-300 mb-15">
        ¡Aprovecha la promoción hasta agotar stock!
      </p>

      <div class="text-5xl font-extrabold mb-2">
        S/ {precioPreventa}
      </div>

      <p class="font-bold text-yellow-300 mb-4 text-xl ">
        Promo 2x70 (S/35 c/u)
      </p>

      <p class="text-gray-400 text-sm mb-6">
        25 promos disponibles (50 entradas)
      </p>

      <button
        on:click={comprarPreventa}
        class="w-full bg-yellow-400 hover:bg-yellow-300 text-black font-bold py-3 rounded-xl transition mt-14"
      >
        COMPRAR
      </button>
    </div>


    <!-- ========================= -->
    <!--      TICKET GENERAL       -->
    <!-- ========================= -->
    <div class="border-2 border-yellow-400 p-8 rounded-2xl bg-[#121212] text-center shadow-2xl">

      <h3 class="text-2xl font-bold text-yellow-400 mb-2 uppercase tracking-wide">
        General
      </h3>

      <p class="text-gray-300 mb-6">
        Elige cuántas entradas quieres comprar.
      </p>

      <!-- Opciones de cantidad -->
      <div class="space-y-3 text-left mx-auto w-fit mb-6">

        <label class="flex items-center gap-3 cursor-pointer">
          <input type="radio" name="general" value="1"
            bind:group={cantidadGeneral}
            class="form-radio text-yellow-400"
          />
          <span>1 entrada (S/40)</span>
        </label>

        <label class="flex items-center gap-3 cursor-pointer">
          <input type="radio" name="general" value="2"
            bind:group={cantidadGeneral}
            class="form-radio text-yellow-400"
          />
          <span>2 entradas (S/80)</span>
        </label>

        <label class="flex items-center gap-3 cursor-pointer">
          <input type="radio" name="general" value="3"
            bind:group={cantidadGeneral}
            class="form-radio text-yellow-400"
          />
          <span>3 entradas (S/120)</span>
        </label>

      </div>

      <!-- PRECIO TOTAL -->
      <div class="text-5xl font-extrabold mb-6">
        S/ {precioGeneral * cantidadGeneral}
      </div>

      <p class="text-gray-400 text-sm mb-6">
        110 entradas generales disponibles
      </p>

      <!-- BOTÓN COMPRAR -->
      <button
        on:click={comprarGeneral}
        class="w-full bg-yellow-400 hover:bg-yellow-300 text-black font-bold py-3 rounded-xl transition"
      >
        COMPRAR
      </button>

    </div>

  </div>

</section>


<!-- ============================================= -->
<!--        SECCIÓN INFORMACIÓN DEL EVENTO        -->
<!-- ============================================= -->

<section class="py-20 px-6 bg-black/60 text-black">

  <div class="flex justify-center mb-10">
    <img 
  src={logo}
  alt="Banner Preventa"
  class="w-72 object-contain mx-auto -my-14"
/>
  </div>

  <div class="max-w-6xl mx-auto grid grid-cols-1 md:grid-cols-2 gap-0  ">

    
    <img src={eventImg} class="w-full h-full object-cover rounded-l-2xl" />
    <div class="glass bg-white/20  p-10  text-white rounded-r-2xl">
      <h3 class="text-3xl font-extrabold mb-6">¡EL FESTIVAL DEL PERÚ!</h3>
      <h4 class="text-4xl font-extrabold mb-4">
        Flora y Fauna en el Teatro
      </h4>
      <p class="leading-relaxed text-white/90">
        Aquí vibra el Perú entero.  
        Un show íntimo, emocional y único.  
        Vive una experiencia inolvidable donde la música cobra vida.
      </p>
    </div>

  </div>

</section>

<style>
  .glass {
    backdrop-filter: blur(15px);
    -webkit-backdrop-filter: blur(15px);
    background: rgba(255,255,255,0.08);
  }


  /* Split-flap animations */
  @keyframes flapDownTop {
    from { transform: rotateX(0deg); }
    50%, to { transform: rotateX(90deg); }
  }

  @keyframes flapDownBottom {
    from, 50% { transform: rotateX(90deg); }
    80% { transform: rotateX(20deg); }
    to { transform: rotateX(0deg); }
  }

  /* Display container */
  .split-flap-display {
    display: flex;
    gap: 12px;
    align-items: center;
    justify-content: center;
    perspective: 1000px;
  }

  /* Digit block */
  .split-flap-digit {
    position: relative;
    width: 70px;
    height: 100px;
    background: #FED314;
    border-radius: 8px;
    overflow: hidden;
    transform-style: preserve-3d;
    border: 2px solid #FED314;
  }

  /* Flap halves */
  .split-flap-part {
    position: absolute;
    inset: 0;
    font-size: 3rem;
    font-weight: 800;
    display: flex;
    align-items: center;
    justify-content: center;
    backface-visibility: hidden;
    background: linear-gradient(#FED314, #FED314);
    color: white;
  }

  .top {
    clip-path: polygon(0 0, 100% 0, 100% 50%, 0 50%);
  }

  .bottom {
    clip-path: polygon(0 50%, 100% 50%, 100% 100%, 0 100%);
  }

  .split-flap-hinge {
    position: absolute;
    top: 50%;
    width: 100%;
    height: 2px;
    transform: translateY(-50%);
    background: #000;
    z-index: 3;
  }

  .animated.final.top {
    animation: flapDownTop 0.35s ease-in forwards;
  }

  .animated.final.bottom {
    animation: flapDownBottom 0.35s ease-out forwards;
  }
</style>
