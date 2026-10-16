<template>
  <div class="eye-wrap" aria-label="Animated JavaScript, Python, and PHP eye">
    <div class="eye" :style="{ backgroundImage: `url(${currentEye})` }">
      <div
        class="eyelid"
        :class="{ 'eyelid-active': active }"
        @animationiteration="changeLanguage"
      ></div>
      <div class="tag">{{ currentTag }}</div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import eyeJS from '@/assets/script eyes.jpg'
import eyePython from '@/assets/script eyes 2.jpeg'
import eyePHP from '@/assets/script eyes 3.jpeg'

defineProps({
  active: {
    type: Boolean,
    default: false,
  },
})

const eyes = [
  { img: eyeJS, tag: 'JAVASCRIPT' },
  { img: eyePython, tag: 'PYTHON' },
  { img: eyePHP, tag: 'PHP' },
]

const index = ref(0)
const currentEye = ref(eyes[0].img)
const currentTag = ref(eyes[0].tag)

const changeLanguage = () => {
  index.value = (index.value + 1) % eyes.length
  currentEye.value = eyes[index.value].img
  currentTag.value = eyes[index.value].tag
}
</script>

<style scoped>
.eye-wrap {
  display: flex;
  width: 100%;
  justify-content: center;
}

.eye {
  position: relative;
  width: min(380px, 100%);
  aspect-ratio: 1;
  overflow: hidden;
  border: 2px solid rgb(255 255 255 / 10%);
  border-radius: 50%;
  background-position: center;
  background-size: 100% 100%;
  box-shadow: 0 0 80px rgb(0 255 136 / 18%);
}

.eyelid {
  position: absolute;
  z-index: 5;
  inset: 0;
  transform: scaleY(1);
  transform-origin: top;
  background: #0a0a0a;
}

.eyelid-active {
  animation: blink 3.5s infinite;
}

.tag {
  position: absolute;
  z-index: 6;
  bottom: 24px;
  left: 50%;
  transform: translateX(-50%);
  border-radius: 9999px;
  background: #6ee7b7;
  padding: 4px 12px;
  color: #000;
  font-size: 10px;
  font-weight: 800;
  letter-spacing: 0.12em;
}

@keyframes blink {
  0%,
  95% {
    transform: scaleY(0);
  }
  97%,
  98% {
    transform: scaleY(1);
  }
  100% {
    transform: scaleY(0);
  }
}

@media (max-width: 500px) {
  .eye {
    width: min(280px, 100%);
  }
}

@media (prefers-reduced-motion: reduce) {
  .eyelid-active {
    animation: none;
    transform: scaleY(0);
  }
}
</style>
