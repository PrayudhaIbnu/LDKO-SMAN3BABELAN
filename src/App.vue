<template>
  <div
    class="min-h-screen flex flex-col bg-white font-sans relative overflow-hidden">

    <!-- HEADER -->
    <!-- <header
      class="bg-white shadow-md border-b border-gray-200 sticky top-0 z-40">
      <div
        class="max-w-5xl mx-auto px-6 py-6 flex items-center justify-between">
        <div class="group">
          <div class="flex items-center gap-3">
            <div class="text-4xl group-hover:scale-110 transition-transform duration-300">📚</div>
            <div>
              <h1 class="text-3xl font-extrabold text-slate-800 tracking-tight">
                Kesekretariatan OSIS
              </h1>
              <p class="text-blue-600 font-medium text-sm">SMA Negeri 1 Jakarta</p>
            </div>
          </div>
        </div>

        <div
          class="px-6 py-3 rounded-2xl bg-blue-50 text-slate-700 font-semibold text-sm shadow-md border border-blue-200 hover:bg-blue-100 transition-all">
          <span class="text-blue-600">Slide</span> {{ currentSlide }} <span class="text-blue-600">dari</span> {{ totalSlides }}
        </div>
      </div>

      <div class="max-w-5xl mx-auto px-6 pb-5">
        <div class="w-full h-3 bg-gray-200 rounded-full overflow-hidden border border-gray-300">
          <div
            class="h-full bg-gradient-to-r from-blue-400 via-blue-500 to-blue-600 rounded-full progress-bar shadow-md"
            :style="{ width: progress + '%' }"></div>
        </div>
      </div>
    </header> -->

    <!-- TOP NAVIGATION (compact) -->
    <header class="fixed w-full top-0 z-40 bg-white border-b border-gray-200">
      <div class="max-w-5xl mx-auto px-4 py-3 flex items-center justify-between gap-4">
        <div class="flex items-center gap-3">
          <div class="text-2xl">📚</div>
          <div>
            <h1 class="text-lg font-semibold text-slate-800">Materi Kesekretariatan OSIS</h1>
            <p class="text-xs text-slate-500">SMA Negeri 3 Babelan</p>
          </div>
        </div>

        <div class="flex items-center gap-4">
          <!-- Slide selector (dropdown) -->
          <label for="slide-select" class="sr-only">Pilih Materi</label>
          <select id="slide-select" v-model.number="currentSlide" @change="onSelectChange" :data-prev="currentSlide" class="text-sm border rounded-md px-3 py-2">
            <option v-for="(s, idx) in slides" :key="idx" :value="idx+1">{{ slideTitles[idx] }}</option>
          </select>

          <!-- small progress badge -->
          <div class="px-3 py-1 rounded-full bg-gray-100 text-sm text-slate-700 border border-gray-200">{{ currentSlide }} / {{ totalSlides }}</div>

          <!-- Next button (ke kanan) -->
          <button @click="next" class="ml-2 inline-flex items-center gap-2 px-3 py-2 rounded-md bg-gradient-to-r from-blue-500 to-blue-600 text-white text-sm">
            <span v-if="currentSlide < totalSlides">Selanjutnya</span>
            <span v-else>Selesai</span>
            <span class="text-sm">→</span>
          </button>
        </div>
      </div>
    </header>

    <!-- CONTENT -->
    <main class="flex-1 mt-16 max-w-5xl mx-auto px-6 py-8 relative z-10">
      <transition :name="direction === 'next' ? 'carousel-next' : 'carousel-prev'" mode="out-in">
        <div
          :key="currentSlide"
          class="bg-white rounded-3xl border border-gray-200 shadow-lg p-10 md:p-14"
        >
          <component
            :is="currentComponent"
            class="block"
            @go="goTo"></component>
        </div>
      </transition>
    </main>

    <!-- footer remains minimal -->

    <!-- FOOTER -->
    <footer class="bg-gradient-to-r from-slate-50 to-blue-50 text-slate-700 py-8 text-center border-t border-gray-200 relative z-10">
      <p class="text-sm font-medium mb-2">
        Semoga pembelajaran ini bermanfaat untuk pengembangan organisasi OSIS! 🌟
      </p>
    </footer>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onBeforeUnmount } from 'vue'

// Import Slides
import SlideWelcome from "./components/SlideWelcome.vue";
import SlideAlur from "./components/SlideAlur.vue";
import SlideSurat from "./components/SlideSurat.vue";
import SlideNotulensi from "./components/SlideNotulensi.vue";
import SlideProposal from "./components/SlideProposal.vue";
import SlideKearsipan from "./components/SlideKearsipan.vue";
import SlideKoordinasi from "./components/SlideKoordinasi.vue";

// Slide array
const slides = [
  SlideWelcome,
  SlideAlur,
  SlideSurat,
  SlideNotulensi,
  SlideProposal,
  SlideKearsipan,
  SlideKoordinasi,
];

const totalSlides = slides.length;
const currentSlide = ref(1)
const direction = ref('next')

// derive simple titles from components (fallback to index)
const slideTitles = slides.map((comp, i) => {
  // try to read a 'title' export on the component, otherwise fallback
  return comp.name || ['Welcome','Alur','Surat','Notulensi','Proposal','Kearsipan','Koordinasi'][i] || `Slide ${i+1}`
})

function onSelectChange(e) {
  // determine direction comparing previous value stored on event (we can read event.target.value)
  const prev = Number(e.target.getAttribute('data-prev')) || 1
  const n = Number(e.target.value)
  direction.value = n > prev ? 'next' : 'prev'
  // store current value back to attr for future comparisons
  e.target.setAttribute('data-prev', String(n))
}

const currentComponent = computed(() => slides[currentSlide.value - 1]);
const progress = computed(() => (currentSlide.value / totalSlides) * 100);



// detect swipe
let startX = 0
let endX = 0

function handleTouchStart(e) {
  startX = e.touches[0].clientX
}

let isSwiping = false

function handleTouchEnd(e) {
  if (isSwiping) return
  isSwiping = true
  setTimeout(() => (isSwiping = false), 350)

  endX = e.changedTouches[0].clientX
  const diff = endX - startX

  if (Math.abs(diff) < 50) return

  if (diff < 0) next()
  else prev()
}


onMounted(() => {
  window.addEventListener('touchstart', handleTouchStart)
  window.addEventListener('touchend', handleTouchEnd)
})

onBeforeUnmount(() => {
  window.removeEventListener('touchstart', handleTouchStart)
  window.removeEventListener('touchend', handleTouchEnd)
})

// ganti direction
function prev() {
  if (currentSlide.value > 1) {
    direction.value = 'prev'
    currentSlide.value--
  }
}

function next() {
  if (currentSlide.value < totalSlides) {
    direction.value = 'next'
    currentSlide.value++
  }
}

function goTo(n) {
  direction.value = n > currentSlide.value ? 'next' : 'prev'
  currentSlide.value = n
}

</script>

<style>
.animate-slide-up {
  animation: slideUp 0.4s ease both;
}

/* ======================================
   BLOB ANIMATION
====================================== */
@keyframes blob {
  0%, 100% {
    transform: translate(0, 0) scale(1);
  }
  33% {
    transform: translate(30px, -50px) scale(1.1);
  }
  66% {
    transform: translate(-20px, 20px) scale(0.9);
  }
}

.animate-blob {
  animation: blob 7s infinite;
}

.animation-delay-2000 {
  animation-delay: 2s;
}

.animation-delay-4000 {
  animation-delay: 4s;
}

/* ======================================
   3D CAROUSEL — SLIDE NEXT
====================================== */
.carousel-next-enter-active,
.carousel-next-leave-active {
  transition: all 0.5s cubic-bezier(0.25, 0.46, 0.45, 1);
}

.carousel-next-enter-from {
  opacity: 0;
  transform: translateX(100px);
}

.carousel-next-leave-to {
  opacity: 0;
  transform: translateX(-100px);
}

/* ======================================
   3D CAROUSEL — SLIDE PREV
====================================== */
.carousel-prev-enter-active,
.carousel-prev-leave-active {
  transition: all 0.5s cubic-bezier(0.25, 0.46, 0.45, 1);
}

.carousel-prev-enter-from {
  opacity: 0;
  transform: translateX(-100px);
}

.carousel-prev-leave-to {
  opacity: 0;
  transform: translateX(100px);
}

@keyframes slideUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.progress-bar {
  transition: width 0.5s cubic-bezier(0.25, 0.46, 0.45, 1);
}
</style>
