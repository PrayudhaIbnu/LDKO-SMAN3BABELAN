<template>
  <div class="text-center space-y-12">
    <div class="relative inline-block mx-auto">
      <div class="absolute inset-0 w-32 h-32 bg-gradient-to-br from-blue-400 to-blue-500 rounded-3xl blur-2xl opacity-20"></div>
      <div class="relative w-32 h-32 rounded-3xl bg-gradient-to-br from-blue-400 to-blue-600 flex items-center justify-center text-white text-6xl shadow-lg animate-float hover:scale-110 transition-transform">
        📚
      </div>
    </div>

    <div class="space-y-4">
      <h2 class="text-5xl font-extrabold text-slate-800 tracking-tight animate-slide-up">
        Selamat Datang! 👋
      </h2>
      <p class="text-xl text-slate-600 font-medium">
        Platform Pembelajaran Interaktif Kesekretariatan OSIS
      </p>
      <p class="text-sm text-slate-500">
        Pelajari semua aspek pengelolaan organisasi dengan cara yang menyenangkan
      </p>
    </div>

    <div class="grid sm:grid-cols-2 lg:grid-cols-3 gap-5 max-w-5xl mx-auto">
      <FeatureCard v-for="(card, idx) in cards" :key="idx" :icon="card.icon" :color="card.color" :title="card.title" :desc="card.desc" :delay="idx * 0.1" />
    </div>

    <div class="pt-6">
      <button @click="goToSlide(2)" class="px-10 py-4 bg-gradient-to-r from-blue-500 to-blue-600 text-white font-bold rounded-2xl text-lg shadow-lg hover:shadow-xl hover:-translate-y-1 transition-all hover:from-blue-600 hover:to-blue-700 inline-flex items-center gap-2">
        <span>Mulai Pembelajaran</span>
        <span class="text-xl">→</span>
      </button>
    </div>
  </div>
</template>

<script setup>
import { defineEmits, ref } from 'vue'

const emit = defineEmits(['go'])

const cards = ref([
  { icon: '📋', color: 'blue', title: 'Alur Birokrasi', desc: 'Memahami langkah-langkah perizinan kegiatan OSIS.' },
  { icon: '✉️', color: 'green', title: 'Surat Menyurat', desc: 'Belajar jenis dan format surat resmi.' },
  { icon: '📝', color: 'purple', title: 'Notulensi', desc: 'Cara mencatat jalannya rapat dengan baik.' },
  { icon: '📊', color: 'orange', title: 'Proposal & LPJ', desc: 'Menyusun proposal dan laporan pertanggungjawaban.' },
  { icon: '🗂️', color: 'red', title: 'Kearsipan', desc: 'Mengelola dan menyimpan dokumen OSIS.' },
  { icon: '🤝', color: 'indigo', title: 'Koordinasi', desc: 'Memahami alur komunikasi organisasi.' },
])

function goToSlide(n) {
  emit('go', n)
}

const FeatureCard = {
  props: ['icon', 'title', 'desc', 'color', 'delay'],
  template: `
    <div class="p-6 rounded-2xl bg-white border border-gray-200 shadow-md hover:shadow-lg cursor-pointer transition-all hover:-translate-y-2 hover:bg-gray-50 group animate-slide-up" :style="{ animationDelay: delay + 's' }">
      <div class="w-14 h-14 rounded-2xl flex items-center justify-center mx-auto mb-4 text-2xl group-hover:scale-110 transition-transform" :class="'bg-gradient-to-br from-' + color + '-400 to-' + color + '-600'">
        {{ icon }}
      </div>
      <h3 class="font-bold text-lg text-slate-800 mb-2">{{ title }}</h3>
      <p class="text-sm text-slate-600">{{ desc }}</p>
    </div>
  `
}
</script>

<style scoped>
@keyframes float {
  0%, 100% { transform: translateY(0px); }
  50% { transform: translateY(-15px); }
}

.animate-float {
  animation: float 3.5s ease-in-out infinite;
}

@keyframes slideUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.animate-slide-up {
  animation: slideUp 0.6s ease-out forwards !important;
  will-change: transform, opacity;
}

div:nth-child(1) .animate-slide-up { animation-delay: 0s; }
div:nth-child(2) .animate-slide-up { animation-delay: 0.1s; }
div:nth-child(3) .animate-slide-up { animation-delay: 0.2s; }
div:nth-child(4) .animate-slide-up { animation-delay: 0.3s; }
div:nth-child(5) .animate-slide-up { animation-delay: 0.4s; }
div:nth-child(6) .animate-slide-up { animation-delay: 0.5s; }
</style>
