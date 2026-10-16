<script setup>
import { ref } from 'vue'
import { Swiper, SwiperSlide } from 'swiper/vue'
import { Autoplay, Navigation, Pagination } from 'swiper/modules'
import EyeBlink from '@/components/EyeBlink.vue'
import 'swiper/css'
import 'swiper/css/navigation'
import 'swiper/css/pagination'

const modules = [Autoplay, Navigation, Pagination]
const contactForm = ref({ name: '', email: '', message: '' })
const messageSent = ref(false)

const skills = [
  { mark: 'JS', name: 'JavaScript', tone: 'text-yellow-300' },
  { mark: 'V', name: 'Vue.js', tone: 'text-emerald-300' },
  { mark: 'PY', name: 'Python', tone: 'text-sky-300' },
  { mark: 'PHP', name: 'PHP', tone: 'text-violet-300' },
  { mark: 'N', name: 'Node.js', tone: 'text-lime-300' },
  { mark: 'SQL', name: 'MySQL', tone: 'text-cyan-300' },
  { mark: 'CSS', name: 'Tailwind CSS', tone: 'text-teal-300' },
  { mark: 'GIT', name: 'Git', tone: 'text-orange-300' },
]

const certifications = Array.from({ length: 6 }, (_, index) => ({
  image: `https://via.placeholder.com/400x280?text=CERTIFICATE+${index + 1}`,
  title: `Professional Certificate ${String(index + 1).padStart(2, '0')}`,
  issuer: 'Learning Institution',
  date: '2025',
}))

const socialLinks = [
  { name: 'GitHub', href: 'https://github.com/', mark: 'GH' },
  { name: 'LinkedIn', href: 'https://www.linkedin.com/', mark: 'in' },
  { name: 'Email', href: 'mailto:hello@purity.dev', mark: '@' },
]

function useCertificateFallback(event, cert) {
  const artwork = `<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 400 280"><defs><linearGradient id="g" x2="1" y2="1"><stop stop-color="#123b31"/><stop offset="1" stop-color="#101217"/></linearGradient></defs><rect width="400" height="280" fill="url(#g)"/><rect x="18" y="18" width="364" height="244" rx="12" fill="none" stroke="#6ee7b7" stroke-opacity=".35"/><circle cx="200" cy="91" r="27" fill="#6ee7b7" fill-opacity=".12" stroke="#6ee7b7" stroke-opacity=".7"/><path d="m188 91 8 8 16-18" fill="none" stroke="#6ee7b7" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"/><text x="200" y="153" fill="#e4e4e7" font-family="Arial,sans-serif" font-size="17" text-anchor="middle">CERTIFICATE ${cert}</text><text x="200" y="181" fill="#6ee7b7" font-family="Arial,sans-serif" font-size="10" letter-spacing="3" text-anchor="middle">PURITY.DEV</text><path d="M153 206h94" stroke="#fff" stroke-opacity=".2"/></svg>`
  event.currentTarget.src = `data:image/svg+xml;charset=UTF-8,${encodeURIComponent(artwork)}`
}

function prepareEmail() {
  const { name, email, message } = contactForm.value
  const subject = encodeURIComponent(`Portfolio message from ${name}`)
  const body = encodeURIComponent(`${message}\n\nFrom: ${name} (${email})`)
  window.location.href = `mailto:hello@purity.dev?subject=${subject}&body=${body}`
  messageSent.value = true
}
</script>
<template>
  <EyeMistReveal @revealed="ready = true" />

  <div :class="ready? 'blur-0 opacity-100' : 'blur-[20px] opacity-0'"
       class="transition-all duration-1000">
    <EyeBlink />
    <CertCarousel />
  </div>
</template>
<template>
  <div class="min-h-screen overflow-hidden bg-[#0a0a0a] text-white">
    <header class="sticky top-0 z-50 border-b border-white/[0.07] bg-[#0a0a0a]/85 backdrop-blur-xl">
      <nav
        class="mx-auto flex max-w-7xl items-center justify-between px-5 py-4 sm:px-8"
        aria-label="Main navigation"
      >
        <a href="#home" class="text-lg font-bold tracking-tight text-white">
          Purity<span class="text-emerald-400">.dev</span>
        </a>
        <div class="hidden items-center gap-8 md:flex">
          <a
            v-for="item in ['Home', 'About', 'Skills', 'Certifications', 'Contact']"
            :key="item"
            :href="`#${item.toLowerCase()}`"
            class="text-sm text-zinc-400 transition hover:text-emerald-300"
            >{{ item }}</a
          >
        </div>
        <a
          href="#contact"
          class="rounded-full border border-emerald-400/40 px-4 py-2 text-xs font-semibold text-emerald-300 transition hover:bg-emerald-300 hover:text-zinc-950 md:hidden"
          >Let's talk</a
        >
      </nav>
      <div class="flex gap-6 overflow-x-auto px-5 pb-3 text-xs md:hidden">
        <a
          v-for="item in ['Home', 'About', 'Skills', 'Certifications', 'Contact']"
          :key="item"
          :href="`#${item.toLowerCase()}`"
          class="shrink-0 text-zinc-400 transition hover:text-emerald-300"
          >{{ item }}</a
        >
      </div>
    </header>

    <main>
      <section
        id="home"
        class="relative mx-auto grid min-h-[calc(100svh-69px)] max-w-7xl items-center gap-10 px-5 py-16 sm:px-8 lg:grid-cols-[1.05fr_0.95fr] lg:gap-8 lg:py-20"
      >
        <div
          class="pointer-events-none absolute -left-48 top-16 h-96 w-96 rounded-full bg-emerald-500/[0.08] blur-[120px]"
        ></div>
        <div class="relative z-10">
          <p
            class="mb-6 flex items-center gap-3 text-xs font-semibold uppercase tracking-[0.24em] text-emerald-300"
          >
            <span class="h-px w-8 bg-emerald-400"></span>
            Fullstack developer
          </p>
          <h1
            class="max-w-2xl text-5xl font-semibold leading-[1.08] tracking-[-0.055em] sm:text-6xl lg:text-7xl"
          >
            I Code What
            <span class="block text-zinc-500">I See<span class="text-emerald-400">.</span></span>
          </h1>
          <p class="mt-7 max-w-lg text-base leading-7 text-zinc-400 sm:text-lg">
            I turn ideas into thoughtful digital experiences, from the first sketch to the final
            line of code.
          </p>
          <p class="mt-3 text-sm font-medium tracking-wide text-zinc-300">
            Fullstack Developer <span class="px-1 text-emerald-400">|</span> JavaScript
            <span class="px-1 text-emerald-400">|</span> Python
            <span class="px-1 text-emerald-400">|</span> PHP
          </p>
          <div class="mt-9 flex flex-wrap gap-3">
            <a
              href="#certifications"
              class="rounded-full bg-emerald-300 px-6 py-3 text-sm font-bold text-zinc-950 transition hover:-translate-y-0.5 hover:bg-emerald-200"
              >View Projects <span aria-hidden="true">↗</span></a
            >
            <a
              href="#contact"
              class="rounded-full border border-white/15 px-6 py-3 text-sm font-semibold text-white transition hover:border-emerald-300/70 hover:text-emerald-200"
              >Contact Me</a
            >
          </div>
          <div class="mt-14 flex items-center gap-3 text-xs text-zinc-500">
            <span class="relative flex h-2 w-2">
              <span
                class="absolute inline-flex h-full w-full animate-ping rounded-full bg-emerald-400 opacity-50"
              ></span>
              <span class="relative inline-flex h-2 w-2 rounded-full bg-emerald-400"></span>
            </span>
            Building for the web
          </div>
        </div>
        <div class="relative flex justify-center lg:justify-end">
          <div
            class="pointer-events-none absolute inset-0 m-auto h-72 w-72 rounded-full border border-emerald-300/10 sm:h-96 sm:w-96"
          ></div>
          <EyeBlink />
        </div>
      </section>

      <section id="about" class="scroll-mt-20 border-y border-white/[0.06] bg-white/[0.015]">
        <div
          class="mx-auto grid max-w-7xl gap-12 px-5 py-24 sm:px-8 md:grid-cols-[0.8fr_1.2fr] md:items-center"
        >
          <div
            class="relative mx-auto aspect-[4/5] w-full max-w-sm overflow-hidden rounded-3xl border border-white/10 bg-gradient-to-br from-emerald-300/10 via-zinc-900 to-zinc-950"
          >
            <div class="absolute inset-5 rounded-2xl border border-dashed border-white/10"></div>
            <div class="absolute inset-0 flex flex-col items-center justify-center text-center">
              <span
                class="mb-4 flex h-20 w-20 items-center justify-center rounded-full border border-emerald-300/30 bg-emerald-300/10 text-3xl text-emerald-200"
                >P.</span
              >
              <span class="text-sm font-medium text-zinc-300">Your portrait goes here</span>
              <span class="mt-1 text-xs text-zinc-600">Add an image to personalize this space</span>
            </div>
            <span class="absolute bottom-8 left-8 font-mono text-xs text-emerald-300/60"
              >&lt;about /&gt;</span
            >
          </div>
          <div>
            <p class="section-kicker">A little about me</p>
            <h2 class="section-title">
              Curious by nature.<br /><span class="text-zinc-500">Builder by choice.</span>
            </h2>
            <p class="mt-7 max-w-2xl leading-8 text-zinc-400">
              I’m a fullstack developer who enjoys shaping clear ideas into useful, polished web
              experiences. I work across the stack with JavaScript, Python, and PHP, and love
              learning the tools that make good products feel effortless.
            </p>
            <a
              href="#contact"
              class="mt-8 inline-flex items-center gap-2 text-sm font-semibold text-emerald-300 transition hover:gap-3"
            >
              Get to know me <span aria-hidden="true">→</span>
            </a>
          </div>
        </div>
      </section>

      <section id="skills" class="scroll-mt-20 mx-auto max-w-7xl px-5 py-24 sm:px-8">
        <div class="mb-12 flex flex-wrap items-end justify-between gap-5">
          <div>
            <p class="section-kicker">Tools of the trade</p>
            <h2 class="section-title">Skills &amp; technologies</h2>
          </div>
          <p class="max-w-sm text-sm leading-6 text-zinc-500">
            A growing toolkit for designing, building, and shipping for the web.
          </p>
        </div>
        <div class="grid grid-cols-2 gap-3 sm:grid-cols-3 lg:grid-cols-4">
          <article
            v-for="skill in skills"
            :key="skill.name"
            class="group flex min-h-32 items-center gap-4 rounded-2xl border border-white/[0.07] bg-white/[0.025] p-5 transition duration-300 hover:-translate-y-1 hover:border-emerald-300/30 hover:bg-emerald-300/[0.04]"
          >
            <span
              class="flex h-12 w-12 shrink-0 items-center justify-center rounded-xl bg-white/[0.06] font-mono text-sm font-bold transition group-hover:bg-emerald-300/10"
              :class="skill.tone"
              >{{ skill.mark }}</span
            >
            <span>
              <span class="block text-sm font-semibold text-zinc-100">{{ skill.name }}</span>
              <span class="mt-1 block text-xs text-zinc-500">Technology</span>
            </span>
          </article>
        </div>
      </section>

      <section
        id="certifications"
        class="scroll-mt-20 border-y border-white/[0.06] bg-white/[0.015]"
      >
        <div class="mx-auto max-w-7xl px-5 py-24 sm:px-8">
          <div class="mb-10 flex flex-wrap items-end justify-between gap-5">
            <div>
              <p class="section-kicker">Learning never stops</p>
              <h2 class="section-title">My Certifications</h2>
            </div>
            <div class="flex gap-2">
              <button
                class="cert-prev flex h-11 w-11 items-center justify-center rounded-full border border-white/10 text-lg text-zinc-300 transition hover:border-emerald-300/50 hover:text-emerald-200"
                aria-label="Previous certifications"
              >
                ←
              </button>
              <button
                class="cert-next flex h-11 w-11 items-center justify-center rounded-full border border-white/10 text-lg text-zinc-300 transition hover:border-emerald-300/50 hover:text-emerald-200"
                aria-label="Next certifications"
              >
                →
              </button>
            </div>
          </div>
          <Swiper
            :modules="modules"
            :slides-per-view="1"
            :space-between="18"
            :loop="true"
            :autoplay="{ delay: 4200, disableOnInteraction: false, pauseOnMouseEnter: true }"
            :navigation="{ prevEl: '.cert-prev', nextEl: '.cert-next' }"
            :pagination="{ clickable: true, el: '.cert-pagination' }"
            :breakpoints="{
              640: { slidesPerView: 2, spaceBetween: 20 },
              1024: { slidesPerView: 3, spaceBetween: 24 },
            }"
            class="cert-swiper !overflow-visible"
          >
            <SwiperSlide v-for="cert in certifications" :key="cert.title" class="h-auto">
              <article
                class="group h-full overflow-hidden rounded-2xl border border-white/10 bg-white/[0.035] backdrop-blur-xl transition duration-300 hover:-translate-y-1 hover:scale-[1.015] hover:border-emerald-300/25"
              >
                <img
                  :src="cert.image"
                  :alt="`${cert.title} certificate preview`"
                  class="aspect-[10/7] w-full border-b border-white/10 bg-zinc-900 object-cover"
                  loading="lazy"
                  @error="useCertificateFallback($event, cert.title.slice(-2))"
                />
                <div class="p-5">
                  <div class="flex items-center justify-between gap-3">
                    <p class="text-xs font-semibold uppercase tracking-[0.15em] text-emerald-300">
                      Certificate
                    </p>
                    <span
                      class="rounded-full border border-white/10 px-2.5 py-1 text-xs text-zinc-400"
                      >{{ cert.date }}</span
                    >
                  </div>
                  <h3 class="mt-4 font-semibold text-white">{{ cert.title }}</h3>
                  <p class="mt-1 text-sm text-zinc-500">{{ cert.issuer }}</p>
                </div>
              </article>
            </SwiperSlide>
          </Swiper>
          <div class="cert-pagination mt-8 flex justify-center gap-2"></div>
        </div>
      </section>

      <section
        id="contact"
        class="scroll-mt-20 mx-auto grid max-w-7xl gap-12 px-5 py-24 sm:px-8 lg:grid-cols-[0.85fr_1.15fr]"
      >
        <div>
          <p class="section-kicker">Have a good one in mind?</p>
          <h2 class="section-title">
            Let’s make<br /><span class="text-zinc-500">something matter.</span>
          </h2>
          <p class="mt-6 max-w-md leading-7 text-zinc-400">
            Tell me what you’re building, what you’re curious about, or just say hello.
          </p>
          <div class="mt-9 flex flex-wrap gap-3">
            <a
              v-for="social in socialLinks"
              :key="social.name"
              :href="social.href"
              target="_blank"
              rel="noreferrer"
              class="inline-flex items-center gap-2 rounded-full border border-white/10 px-4 py-2.5 text-sm text-zinc-300 transition hover:border-emerald-300/40 hover:text-emerald-200"
              ><span class="font-mono text-xs text-emerald-300">{{ social.mark }}</span
              >{{ social.name }}</a
            >
          </div>
        </div>
        <form
          class="rounded-3xl border border-white/10 bg-white/[0.03] p-6 sm:p-8"
          @submit.prevent="prepareEmail"
        >
          <div class="grid gap-5 sm:grid-cols-2">
            <label class="form-label"
              >Your name
              <input
                v-model.trim="contactForm.name"
                required
                name="name"
                autocomplete="name"
                class="form-input"
                placeholder="Jane Doe"
              />
            </label>
            <label class="form-label"
              >Email address
              <input
                v-model.trim="contactForm.email"
                required
                type="email"
                name="email"
                autocomplete="email"
                class="form-input"
                placeholder="jane@example.com"
              />
            </label>
          </div>
          <label class="form-label mt-5 block"
            >Your message
            <textarea
              v-model.trim="contactForm.message"
              required
              name="message"
              rows="5"
              class="form-input resize-y"
              placeholder="Tell me a little about your project..."
            ></textarea>
          </label>
          <div class="mt-6 flex flex-wrap items-center gap-4">
            <button
              type="submit"
              class="rounded-full bg-emerald-300 px-6 py-3 text-sm font-bold text-zinc-950 transition hover:bg-emerald-200"
            >
              Send a message <span aria-hidden="true">↗</span>
            </button>
            <p v-if="messageSent" role="status" class="text-sm text-emerald-300">
              Your email draft is ready.
            </p>
          </div>
        </form>
      </section>
    </main>

    <footer class="border-t border-white/[0.07]">
      <div
        class="mx-auto flex max-w-7xl flex-col gap-3 px-5 py-7 text-xs text-zinc-500 sm:flex-row sm:items-center sm:justify-between sm:px-8"
      >
        <a href="#home" class="text-sm font-semibold text-zinc-300"
          >Purity<span class="text-emerald-400">.dev</span></a
        >
        <p>Designed with curiosity. Built with care.</p>
        <p>© {{ new Date().getFullYear() }} Purity. All rights reserved.</p>
      </div>
    </footer>
  </div>
</template>

<style>
html {
  scroll-behavior: smooth;
  scroll-padding-top: 5rem;
}

body {
  background: #0a0a0a;
}

.section-kicker {
  margin-bottom: 0.9rem;
  color: #6ee7b7;
  font-size: 0.7rem;
  font-weight: 700;
  letter-spacing: 0.2em;
  text-transform: uppercase;
}

.section-title {
  font-size: clamp(2rem, 4vw, 3.1rem);
  font-weight: 600;
  letter-spacing: -0.055em;
  line-height: 1.12;
}

.form-label {
  color: #d4d4d8;
  font-size: 0.875rem;
  font-weight: 500;
}

.form-input {
  margin-top: 0.65rem;
  display: block;
  width: 100%;
  border: 1px solid rgb(255 255 255 / 10%);
  border-radius: 0.8rem;
  background: rgb(255 255 255 / 3%);
  padding: 0.85rem 1rem;
  color: white;
  outline: none;
  transition: border-color 180ms ease;
}

.form-input::placeholder {
  color: #62626b;
}

.form-input:focus {
  border-color: rgb(110 231 183 / 55%);
}

.cert-pagination .swiper-pagination-bullet {
  width: 7px;
  height: 7px;
  background: #71717a;
  opacity: 1;
  transition:
    width 180ms ease,
    background-color 180ms ease;
}

.cert-pagination .swiper-pagination-bullet-active {
  width: 22px;
  border-radius: 9999px;
  background: #6ee7b7;
}

@media (prefers-reduced-motion: reduce) {
  html {
    scroll-behavior: auto;
  }
}
</style>
