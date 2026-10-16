<script setup>
import { ref } from 'vue'

const emit = defineEmits(['light-change'])
const lightOn = ref(false)

function toggleLight() {
  lightOn.value = !lightOn.value
  emit('light-change', lightOn.value)
}
</script>

<template>
  <div class="light-control">
    <button
      class="bell-switch"
      :class="{ 'light-on': lightOn }"
      type="button"
      :aria-label="lightOn ? 'Switch the light off' : 'Switch the light on'"
      :aria-pressed="lightOn"
      @click="toggleLight"
    >
      <span class="bell-rope"></span>
      <span class="bell-cap"></span>
      <span class="bell-body"></span>
      <span class="bell-highlight"></span>
      <span class="bell-rim"></span>
      <span class="bell-bulb"></span>
      <span class="bell-rays"></span>
      <span class="light-beam"></span>
    </button>
    <div class="social-links" aria-label="Social links">
      <a
        class="social-link"
        href="https://github.com/"
        target="_blank"
        rel="noreferrer"
        aria-label="GitHub"
        title="GitHub"
      >
        <svg viewBox="0 0 24 24" aria-hidden="true">
          <path
            fill="currentColor"
            d="M12 .9a11.1 11.1 0 0 0-3.51 21.63c.56.1.76-.24.76-.54v-2.1c-3.1.67-3.76-1.32-3.76-1.32-.5-1.28-1.24-1.62-1.24-1.62-1.02-.7.08-.69.08-.69 1.12.08 1.7 1.15 1.7 1.15 1 .1.65 2.86 4.5 2.18.1-.73.4-1.22.72-1.5-2.48-.28-5.08-1.24-5.08-5.52 0-1.22.44-2.22 1.15-3-.12-.29-.5-1.43.11-2.98 0 0 .94-.3 3.05 1.15a10.6 10.6 0 0 1 5.55 0c2.12-1.45 3.05-1.15 3.05-1.15.61 1.55.23 2.69.12 2.98.71.78 1.14 1.78 1.14 3.01 0 4.29-2.61 5.23-5.1 5.5.4.35.76 1.03.76 2.08v3.08c0 .3.2.65.77.54A11.1 11.1 0 0 0 12 .9Z"
          />
        </svg>
      </a>
      <a
        class="social-link"
        href="https://www.linkedin.com/"
        target="_blank"
        rel="noreferrer"
        aria-label="LinkedIn"
        title="LinkedIn"
      >
        <svg viewBox="0 0 24 24" aria-hidden="true">
          <path
            fill="currentColor"
            d="M20.45 2H3.55C2.69 2 2 2.68 2 3.52v16.96c0 .84.69 1.52 1.55 1.52h16.9c.86 0 1.55-.68 1.55-1.52V3.52c0-.84-.69-1.52-1.55-1.52ZM7.93 18.74H4.98V9.25h2.95v9.49ZM6.46 7.95a1.71 1.71 0 1 1 0-3.42 1.71 1.71 0 0 1 0 3.42Zm12.28 10.79h-2.94v-4.62c0-1.1-.02-2.52-1.54-2.52-1.55 0-1.79 1.2-1.79 2.44v4.7H9.53V9.25h2.82v1.3h.04c.39-.74 1.35-1.53 2.78-1.53 2.98 0 3.57 1.96 3.57 4.5v5.22Z"
          />
        </svg>
      </a>
      <a class="social-link" href="mailto:hello@purity.dev" aria-label="Email" title="Email">
        <svg viewBox="0 0 24 24" aria-hidden="true">
          <path
            fill="currentColor"
            d="M3.5 4h17A2.5 2.5 0 0 1 23 6.5v11a2.5 2.5 0 0 1-2.5 2.5h-17A2.5 2.5 0 0 1 1 17.5v-11A2.5 2.5 0 0 1 3.5 4Zm8.5 8.1 8.34-5.48a.5.5 0 0 0-.27-.92H3.93a.5.5 0 0 0-.27.92L12 12.1Zm-9 5.4a1 1 0 0 0 1 1h16a1 1 0 0 0 1-1v-8.5l-8.45 5.55a1 1 0 0 1-1.1 0L3 9v8.5Z"
          />
        </svg>
      </a>
    </div>
    <span class="light-status" aria-live="polite">
      <span class="status-indicator" :class="{ 'status-on': lightOn }"></span>
      LIGHT {{ lightOn ? 'ON' : 'OFF' }}
    </span>
  </div>
</template>

<style scoped>
.light-control {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.7rem;
}

.bell-switch {
  position: relative;
  width: min(64vw, 190px);
  aspect-ratio: 1;
  overflow: visible;
  border: 0;
  border-radius: 50%;
  background: transparent;
  cursor: pointer;
  isolation: isolate;
}

.bell-switch:focus-visible,
.social-link:focus-visible {
  outline: 2px solid #6ee7b7;
  outline-offset: 5px;
}

.bell-rope {
  position: absolute;
  top: -10%;
  left: 50%;
  width: 3px;
  height: 52%;
  transform: translateX(-50%);
  transform-origin: top;
  background: linear-gradient(90deg, #252525, #aaa, #252525);
}

.bell-cap {
  position: absolute;
  top: 17%;
  left: 42%;
  width: 16%;
  aspect-ratio: 1;
  border: 1px solid #ffffff40;
  border-radius: 50%;
  background: linear-gradient(110deg, #555, #d2ceca 45%, #3e4147);
  box-shadow: 0 0 12px #bfeaff38;
}

.bell-body {
  position: absolute;
  top: 29%;
  left: 20%;
  width: 60%;
  height: 48%;
  border: 1px solid #ffffff47;
  border-radius: 48% 48% 35% 35% / 40% 40% 25% 25%;
  background: linear-gradient(100deg, #202329 2%, #b7b5b4 42%, #55565a 72%, #151619);
  box-shadow:
    inset 8px 0 14px #5d819666,
    inset -9px 0 14px #fff7,
    0 2px 12px #c6eaffa8;
  transition:
    filter 400ms ease,
    box-shadow 400ms ease,
    background 400ms ease;
}

.bell-highlight {
  position: absolute;
  top: 36%;
  left: 33%;
  width: 30%;
  height: 35%;
  transform: rotate(12deg);
  border-radius: 50%;
  background: #ffffff26;
  filter: blur(9px);
  pointer-events: none;
}

.bell-rim {
  position: absolute;
  top: 71%;
  left: 16%;
  width: 68%;
  height: 13%;
  border: 1px solid #ffffff8a;
  border-radius: 50%;
  background: linear-gradient(90deg, #181818, #dedbd5 50%, #1c1c1c);
  box-shadow:
    0 3px 12px #000,
    inset 0 2px 4px #ffffffa6;
}

.bell-bulb {
  position: absolute;
  z-index: 2;
  top: 76%;
  left: 24%;
  width: 52%;
  height: 13%;
  border-radius: 50%;
  background: #181818;
  box-shadow: inset 0 0 10px #000;
  transition:
    background 400ms ease,
    box-shadow 400ms ease;
}

.bell-rays {
  position: absolute;
  z-index: -1;
  top: 43%;
  left: 50%;
  width: 30%;
  aspect-ratio: 1;
  transform: translate(-50%, -50%);
  border-radius: 50%;
  background: repeating-conic-gradient(#fff5 0deg 1deg, transparent 2deg 12deg);
  opacity: 0;
  transition: opacity 400ms ease;
}

.light-beam {
  position: absolute;
  z-index: -2;
  top: 50%;
  left: 50%;
  width: 130%;
  height: 100%;
  transform: translate(-50%, 0);
  clip-path: polygon(38% 0, 62% 0, 100% 100%, 0 100%);
  background: linear-gradient(180deg, #ffe9d455, transparent 80%);
  filter: blur(12px);
  opacity: 0;
  pointer-events: none;
  transition: opacity 400ms ease;
}

.light-on .bell-body {
  background: linear-gradient(100deg, #35332e 2%, #fff1cf 42%, #a7875f 72%, #30261e);
  box-shadow:
    inset 8px 0 14px #fff2,
    inset -9px 0 14px #fff9,
    0 0 24px #ffe9d466;
}

.light-on .bell-bulb {
  background: #fff8e9;
  box-shadow:
    0 0 12px 5px #ffe9d4,
    0 0 38px 12px #ce6e1a99,
    inset 0 0 10px white;
}

.light-on .bell-rays,
.light-on .light-beam {
  opacity: 0.8;
}

.bell-switch.light-on {
  animation: ring-bell 900ms ease-in-out 2;
}

.social-links {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.65rem;
}

.social-link {
  display: inline-flex;
  width: 2.35rem;
  height: 2.35rem;
  align-items: center;
  justify-content: center;
  border: 1px solid rgb(255 255 255 / 12%);
  border-radius: 50%;
  background: rgb(255 255 255 / 3%);
  color: #a1a1aa;
  transition:
    color 180ms ease,
    border-color 180ms ease,
    background-color 180ms ease,
    transform 180ms ease;
}

.social-link:hover {
  transform: translateY(-2px);
  border-color: rgb(110 231 183 / 55%);
  background: rgb(110 231 183 / 8%);
  color: #a7f3d0;
}

.social-link svg {
  width: 1rem;
  height: 1rem;
}

.light-status {
  display: flex;
  align-items: center;
  gap: 0.45rem;
  color: #71717a;
  font-family: ui-monospace, monospace;
  font-size: 0.6rem;
  letter-spacing: 0.15em;
}

.status-indicator {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: #52525b;
  transition:
    background-color 300ms ease,
    box-shadow 300ms ease;
}

.status-on {
  background: #6ee7b7;
  box-shadow: 0 0 10px #6ee7b7;
}

@keyframes ring-bell {
  0%,
  100% {
    rotate: 0deg;
  }

  25% {
    rotate: 0.8deg;
  }

  75% {
    rotate: -0.8deg;
  }
}

@media (prefers-reduced-motion: reduce) {
  .light-on .bell-switch {
    animation: none;
  }
}
</style>
