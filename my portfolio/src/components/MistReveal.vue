<template>
  <div v-if="show" class="mist-overlay" :class="{ 'wipe-out': wiping }">
    <!-- misty blurred background -->
    <div class="mist"></div>

    <!-- the wiper that clears it - like a hand wiping glass -->
    <div class="wiper"></div>

    <!-- Your eye faintly behind mist -->
    <div class="hint">wiping...</div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
const emit = defineEmits(['revealed'])
const show = ref(true)
const wiping = ref(false)

onMounted(() => {
  // start wipe after 1.2s
  setTimeout(() => {
    wiping.value = true
    // remove overlay after wipe animation
    setTimeout(() => {
      show.value = false
      emit('revealed')
    }, 1200)
  }, 1200)
})
</script>

<style scoped>
.mist-overlay{
  position:fixed; inset:0;
  z-index:9999;
  background: rgba(10,10,10,0.85);
  backdrop-filter: blur(25px);
  overflow:hidden;
}
.mist{
  position:absolute; inset:-50%;
  background: radial-gradient(circle at 50% 50%, rgba(255,255,255,0.15), transparent 60%),
              url('https://grainy-gradients.vercel.app/noise.svg');
  opacity:0.6;
  animation: drift 4s infinite alternate;
}
@keyframes drift{
  from{ transform: translate(-10px, -10px) scale(1.1); }
  to{ transform: translate(10px, 10px) scale(1); }
}
.wiper{
  position:absolute;
  top:0; left:-30%;
  width:40%; height:100%;
  background: linear-gradient(90deg, transparent, rgba(255,255,255,0.4), transparent);
  backdrop-filter: blur(0px);
  transform: skewX(-15deg);
  animation: wipe 1.2s ease-in-out forwards;
  animation-delay: 1.2s;
}
@keyframes wipe{
  0%{ left:-30%; }
  100%{ left:130%; }
}
.wipe-out{
  animation: clearMist 1.2s ease-in-out forwards;
  animation-delay: 1.3s;
}
@keyframes clearMist{
  0%{ backdrop-filter: blur(25px); opacity:1; }
  100%{ backdrop-filter: blur(0px); opacity:0; }
}
.hint{
  position:absolute; bottom:40px; left:50%;
  transform:translateX(-50%);
  color:rgba(255,255,255,0.5);
  font-family:monospace; font-size:12px; letter-spacing:3px;
}
</style>