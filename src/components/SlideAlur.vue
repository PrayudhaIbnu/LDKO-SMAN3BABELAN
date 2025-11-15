<template>
  <div class="space-y-12">
    <!-- HEADER -->
    <header class="text-center space-y-4 animate-fade-up">
      <div class="flex items-center justify-center gap-3">
        <span class="text-5xl">📋</span>
        <h2 class="text-4xl font-extrabold text-slate-800">
          Alur Birokrasi Izin Kegiatan
        </h2>
      </div>
      <p class="text-lg text-slate-600 max-w-2xl mx-auto">
        Proses resmi sebelum kegiatan OSIS dapat berjalan dengan tertib dan aman
      </p>
    </header>

    <!-- =====================
         MODE 1: STEP BY STEP (Interactive)
    ====================== -->
    <div v-if="!showFullTimeline" class="animate-fade-up">
      <!-- Progress Bar -->
      <div class="max-w-xl mx-auto mb-8">
        <div class="flex items-center justify-between mb-3">
          <span class="text-sm font-semibold text-slate-700">
            Langkah {{ currentIndex + 1 }} dari {{ steps.length }}
          </span>
          <span class="text-xs text-slate-500">{{ Math.round((currentIndex + 1) / steps.length * 100) }}%</span>
        </div>
        <div class="w-full h-2 bg-slate-200 rounded-full overflow-hidden">
          <div 
            class="h-full bg-gradient-to-r from-blue-500 to-blue-600 rounded-full transition-all duration-500"
            :style="{ width: ((currentIndex + 1) / steps.length * 100) + '%' }"
          ></div>
        </div>
      </div>

      <!-- ACTIVE STEP CARD -->
      <div class="max-w-2xl mx-auto">
        <div class="bg-white rounded-2xl border-2 border-slate-200 p-10 shadow-lg hover:shadow-xl transition-shadow">
          
          <!-- Badge -->
          <div class="relative mb-8">
            <div class="absolute inset-0 w-24 h-24 bg-blue-400 blur-2xl opacity-40 mx-auto"></div>
            <div class="relative w-24 h-24 mx-auto flex items-center justify-center rounded-full
                        bg-gradient-to-br from-blue-500 to-blue-600 text-white text-5xl font-bold
                        shadow-xl ring-4 ring-blue-100 animate-pop">
              {{ currentIndex + 1 }}
            </div>
          </div>

          <!-- Content -->
          <div class="text-center space-y-4">
            <h3 class="text-3xl font-bold text-slate-800">
              {{ steps[currentIndex].title }}
            </h3>
            <p class="text-lg text-slate-600 leading-relaxed">
              {{ steps[currentIndex].desc }}
            </p>
          </div>

          <!-- Indicator Dots -->
          <div class="flex justify-center gap-2 mt-8">
            <button
              v-for="(_, idx) in steps"
              :key="idx"
              @click="currentIndex = idx"
              :class="[
                'w-3 h-3 rounded-full transition-all duration-300',
                idx === currentIndex 
                  ? 'w-8 bg-blue-600' 
                  : 'bg-slate-300 hover:bg-slate-400'
              ]"
              :aria-label="`Langkah ${idx + 1}`"
            ></button>
          </div>
        </div>
      </div>

      <!-- ACTION BUTTONS -->
      <div class="flex justify-center gap-4 mt-10">
        <button
          @click="prev"
          :disabled="currentIndex === 0"
          class="px-6 py-3 rounded-xl border-2 border-slate-300 bg-white text-slate-700 font-semibold
                 shadow-md hover:shadow-lg hover:border-slate-400 disabled:opacity-50 disabled:cursor-not-allowed
                 transition-all hover:-translate-y-1 duration-200">
          ← Kembali
        </button>

        <button
          v-if="currentIndex < steps.length - 1"
          @click="next"
          class="px-8 py-3 rounded-xl bg-gradient-to-r from-blue-600 to-blue-700 text-white font-semibold
                 shadow-lg hover:shadow-xl hover:-translate-y-1 transition-all duration-200">
          Lanjut →
        </button>

        <button
          v-else
          @click="finish"
          class="px-8 py-3 rounded-xl bg-gradient-to-r from-green-600 to-green-700 text-white font-semibold
                 shadow-lg hover:shadow-xl hover:-translate-y-1 transition-all duration-200 flex items-center gap-2">
          <span>Lihat Alur Lengkap</span>
          <span>→</span>
        </button>
      </div>
    </div>

    <!-- =====================
         MODE 2: FULL TIMELINE
    ====================== -->
    <div v-else class="animate-fade-up">
      <!-- Back Button -->
      <div class="mb-8">
        <button
          @click="showFullTimeline = false; currentIndex = 0"
          class="px-4 py-2 rounded-lg border border-slate-300 bg-white text-slate-700 text-sm font-semibold
                 hover:bg-slate-50 transition-all">
          ← Kembali ke Mode Interaktif
        </button>
      </div>

      <h3 class="text-3xl font-extrabold text-center text-slate-800 mb-12">
        🎉 Alur Lengkap Birokrasi Perizinan Kegiatan
      </h3>

      <!-- FULL TIMELINE -->
      <div class="max-w-7xl mx-auto px-4 overflow-x-auto">
        <div class="relative py-12 pb-20 min-w-max">

          <!-- Connecting Line -->
          <svg
            class="absolute top-6 left-0 pointer-events-none"
            :width="svgWidth"
            height="60"
            style="overflow: visible"
          >
            <defs>
              <linearGradient id="lineGradient" x1="0%" y1="50%" x2="100%" y2="50%">
                <stop offset="0%" stop-color="#93c5fd" stop-opacity="0.3"/>
                <stop offset="50%" stop-color="#3b82f6" stop-opacity="0.9"/>
                <stop offset="100%" stop-color="#93c5fd" stop-opacity="0.3"/>
              </linearGradient>
            </defs>
            <path
              :d="generatePath()"
              fill="none"
              stroke="url(#lineGradient)"
              stroke-width="6"
              stroke-linecap="round"
            />
          </svg>

          <!-- STEPS -->
          <div class="flex gap-6 relative">
            <div
              v-for="(step, idx) in steps"
              :key="idx"
              class="flex flex-col items-center animate-fade-up"
              :style="{ animationDelay: (idx * 0.1) + 's' }"
            >
              <!-- Badge -->
              <div class="relative mb-8 z-10">
                <div class="absolute inset-0 w-16 h-16 bg-blue-400 rounded-full blur-xl opacity-40"></div>
                <div class="relative w-16 h-16 flex items-center justify-center rounded-full
                            bg-gradient-to-br from-blue-500 to-blue-600 text-white text-xl font-bold
                            shadow-lg ring-4 ring-white hover:scale-110 transition-transform cursor-pointer">
                  {{ idx + 1 }}
                </div>
              </div>

              <!-- Arrow Down -->
              <div class="text-2xl text-blue-400 mb-3 animate-bounce" :style="{ animationDelay: (idx * 0.15) + 's' }">
                ↓
              </div>

              <!-- Card -->
              <div class="bg-white border-2 border-slate-200 rounded-xl p-6 w-56 shadow-md 
                          hover:shadow-lg hover:border-blue-300 transition-all duration-300 group">
                <h4 class="font-bold text-slate-800 text-sm mb-3 group-hover:text-blue-600 transition-colors line-clamp-2">
                  {{ step.title }}
                </h4>
                <p class="text-xs text-slate-600 leading-relaxed line-clamp-3">
                  {{ step.desc }}
                </p>
              </div>
            </div>
          </div>

        </div>
      </div>

      <!-- Info Box -->
      <div class="max-w-3xl mx-auto mt-12 animate-fade-up" style="animation-delay: 0.6s">
        <div class="bg-gradient-to-r from-blue-50 to-indigo-50 border-l-4 border-blue-500 rounded-lg p-6 shadow-sm">
          <div class="flex gap-4">
            <span class="text-3xl flex-shrink-0">💡</span>
            <div>
              <h4 class="font-bold text-slate-800 mb-2">Catatan Penting</h4>
              <p class="text-slate-600 text-sm">
                Setiap tahap harus dilakukan dengan tertib dan tepat waktu. Keterlambatan dalam proses dapat menunda pelaksanaan kegiatan OSIS Anda.
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Bottom Spacing -->
    <div class="h-8"></div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue"

const steps = ref([
  { 
    title: "Perencanaan Kegiatan", 
    desc: "Menentukan konsep, tujuan, target peserta, waktu & tempat kegiatan dengan detail yang jelas." 
  },
  { 
    title: "Penyusunan Proposal", 
    desc: "Berisi latar belakang, tujuan, rundown acara, anggaran & struktur panitia yang lengkap." 
  },
  { 
    title: "Pengajuan ke Pembina OSIS", 
    desc: "Pembina memeriksa proposal agar kegiatan aman dan sesuai dengan aturan sekolah." 
  },
  { 
    title: "Pengajuan Izin Kepala Sekolah", 
    desc: "Disahkan oleh Kepala Sekolah secara resmi sebelum kegiatan dilaksanakan." 
  },
  { 
    title: "Pelaksanaan & LPJ", 
    desc: "Kegiatan berlangsung sesuai rencana dan dibuat Laporan Pertanggungjawaban (LPJ)." 
  }
])

const currentIndex = ref(0)
const showFullTimeline = ref(false)

function next() {
  if (currentIndex.value < steps.value.length - 1) {
    currentIndex.value++
  }
}

function prev() {
  if (currentIndex.value > 0) {
    currentIndex.value--
  }
}

function finish() {
  showFullTimeline.value = true
}

const svgWidth = computed(() => {
  return steps.value.length * 176 + 20 // 176 = card width (224px / 4) + gap
})

const generatePath = () => {
  const stepWidth = 176
  let d = `M 40,30`
  for (let i = 1; i < steps.value.length; i++) {
    d += ` L ${i * stepWidth + 40},30`
  }
  return d
}
</script>

<style scoped>
/* Fade Up */
@keyframes fadeUp {
  from { 
    opacity: 0; 
    transform: translateY(24px); 
  }
  to { 
    opacity: 1; 
    transform: translateY(0); 
  }
}

.animate-fade-up {
  animation: fadeUp 0.6s ease-out forwards;
}

/* Pop */
@keyframes pop {
  0% { 
    transform: scale(0.6); 
    opacity: 0; 
  }
  100% { 
    transform: scale(1); 
    opacity: 1; 
  }
}

.animate-pop { 
  animation: pop 0.4s ease-out; 
}

/* Bounce */
@keyframes bounce {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-8px);
  }
}

.animate-bounce {
  animation: bounce 2s infinite;
}

/* Smooth scrollbar */
::-webkit-scrollbar {
  height: 6px;
}

::-webkit-scrollbar-track {
  background: #f1f5f9;
  border-radius: 3px;
}

::-webkit-scrollbar-thumb {
  background: #cbd5e1;
  border-radius: 3px;
}

::-webkit-scrollbar-thumb:hover {
  background: #94a3b8;
}

/* Utilities */
.line-clamp-2 {
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.line-clamp-3 {
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
</style>