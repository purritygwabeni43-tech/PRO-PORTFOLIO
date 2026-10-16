<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'

const emit = defineEmits(['revealed'])
const visible = ref(true)
const fading = ref(false)
let revealTimeout
let removeTimeout

onMounted(() => {
  // Keep the full-page cover mounted through the complete three-second reveal.
  revealTimeout = window.setTimeout(() => {
    emit('revealed')
    fading.value = true
    removeTimeout = window.setTimeout(() => {
      visible.value = false
    }, 1000)
  }, 3000)
})

onBeforeUnmount(() => {
  window.clearTimeout(revealTimeout)
  window.clearTimeout(removeTimeout)
})
</script>

<template>
  <div
    v-if="visible"
    class="fixed inset-0 z-[9999] overflow-hidden bg-[rgba(10,10,10,0.85)] transition-opacity duration-1000"
    :class="{ 'opacity-0': fading }"
    aria-label="Revealing page"
    role="status"
  >
    <div class="glass-layer absolute inset-0"></div>
    <div class="mist-layer absolute -inset-1/2"></div>
    <div class="evaporation-layer pointer-events-none absolute inset-0 overflow-hidden">
      <span class="evaporating-blob blob-one"></span>
      <span class="evaporating-blob blob-two"></span>
      <span class="evaporating-blob blob-three"></span>
      <span class="evaporating-blob blob-four"></span>
    </div>
    <div class="condensation-layer pointer-events-none absolute inset-0"></div>
    <div class="wiper absolute left-[-30%] top-0 h-full w-[40%]"></div>
  </div>
</template>

<style scoped>
.glass-layer {
  z-index: 0;
  background: rgb(10 10 10 / 18%);
  backdrop-filter: blur(25px);
  animation: clear-mist 1.2s ease-in-out 1.3s forwards;
}

.mist-layer {
  z-index: 1;
  background:
    radial-gradient(ellipse at 25% 35%, rgb(225 237 231 / 22%), transparent 48%),
    radial-gradient(ellipse at 75% 65%, rgb(189 211 203 / 18%), transparent 52%),
    url('https://grainy-gradients.vercel.app/noise.svg');
  background-size:
    auto,
    auto,
    180px 180px;
  opacity: 0.6;
  animation: mist-drift 4s ease-in-out infinite alternate;
}

.condensation-layer {
  z-index: 2;
  background-image: radial-gradient(rgb(255 255 255 / 80%) 1px, transparent 1px);
  background-size: 20px 20px;
  opacity: 0.6;
}

.evaporation-layer {
  z-index: 3;
}

.evaporating-blob {
  position: absolute;
  bottom: -5rem;
  width: clamp(3rem, 9vw, 8rem);
  aspect-ratio: 1;
  border-radius: 50%;
  background: rgb(255 255 255 / 13%);
  filter: blur(20px);
  animation: evaporate 4.8s ease-out infinite;
}

.blob-one {
  left: 12%;
  animation-delay: 0.1s;
}

.blob-two {
  left: 36%;
  width: clamp(4rem, 12vw, 10rem);
  animation-delay: 1.5s;
}

.blob-three {
  left: 67%;
  animation-delay: 2.8s;
}

.blob-four {
  left: 86%;
  width: clamp(2.5rem, 7vw, 6rem);
  animation-delay: 0.9s;
}

.wiper {
  z-index: 4;
  background: linear-gradient(90deg, transparent, rgb(255 255 255 / 40%), transparent);
  backdrop-filter: blur(0);
  transform: skewX(-15deg);
  animation: wipe 1.2s ease-in-out 1.2s forwards;
}

@keyframes mist-drift {
  from {
    transform: translate(-10px, -10px) scale(1.1);
  }

  to {
    transform: translate(10px, 10px) scale(1);
  }
}

@keyframes evaporate {
  0% {
    opacity: 0;
    transform: translate3d(0, 0, 0) scale(0.7);
  }

  20% {
    opacity: 0.6;
  }

  100% {
    opacity: 0;
    transform: translate3d(2rem, -120vh, 0) scale(1.5);
  }
}

@keyframes wipe {
  from {
    left: -30%;
  }

  to {
    left: 130%;
  }
}

@keyframes clear-mist {
  from {
    backdrop-filter: blur(25px);
    opacity: 1;
  }

  to {
    backdrop-filter: blur(0);
    opacity: 0;
  }
}
</style>
