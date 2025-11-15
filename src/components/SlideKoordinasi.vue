<template>
  <div class="space-y-20">

    <!-- HEADER -->
    <div class="text-center space-y-4 animate-fade-up">
      <div class="inline-flex items-center gap-3 px-5 py-2 bg-pink-50 text-pink-700 rounded-full font-semibold shadow-sm border border-pink-200">
        🤝 Koordinasi Struktur OSIS
      </div>

      <h2 class="text-4xl font-extrabold text-slate-800 tracking-tight">
        Alur Komunikasi OSIS
      </h2>

      <p class="text-slate-600 text-lg max-w-2xl mx-auto leading-relaxed">
        Visualisasi alur komunikasi OSIS dengan gaya yang lebih modern & lembut.
      </p>
    </div>


    <!-- SOFT PASTEL FLOW -->
    <div class="relative max-w-xl mx-auto px-10">

      <!-- Vertical dotted line -->
      <div class="absolute left-1/2 top-0 bottom-0 border-l-2 border-dashed border-slate-300"></div>

      <div
        v-for="(item, idx) in flow"
        :key="idx"
        class="relative flex flex-col items-center text-center animate-bubble"
        :style="{ animationDelay: (idx * 0.15) + 's' }"
      >
        <!-- Bubble -->
        <div
          class="w-[180px] py-6 px-4 rounded-3xl shadow-xl backdrop-blur-md relative z-10 border border-white/30"
          :class="item.bg"
        >
          <div class="text-4xl mb-3">{{ item.emoji }}</div>

          <h3 class="text-xl font-bold text-slate-800 mb-1">
            {{ item.title }}
          </h3>

          <p class="text-slate-600 text-sm">
            {{ item.subtitle }}
          </p>
        </div>

        <!-- Connector spacing -->
        <div v-if="idx < flow.length - 1" class="h-14"></div>
      </div>
    </div>



    <!-- CARDS SECTION -->
    <div class="max-w-6xl mx-auto grid md:grid-cols-2 gap-10 px-6">

      <!-- Card 1 -->
      <div class="group relative bg-white rounded-3xl p-10 shadow-md border border-slate-200 transition-all hover:shadow-xl hover:-translate-y-1">
        <div class="absolute inset-0 bg-blue-200 rounded-3xl opacity-0 group-hover:opacity-20 transition-all"></div>

        <div class="relative z-10 space-y-5">
          <h3 class="text-2xl font-extrabold text-slate-800 flex items-center gap-3">
            <span class="text-3xl">📋</span>
            Tugas Koordinasi
          </h3>

          <ul class="text-slate-700 space-y-3 text-[15px] leading-relaxed">
            <li class="flex gap-3"><span class="text-blue-400 font-bold">•</span> Menyampaikan informasi resmi ke ekstrakurikuler.</li>
            <li class="flex gap-3"><span class="text-blue-400 font-bold">•</span> Melaporkan kegiatan OSIS ke pembina.</li>
            <li class="flex gap-3"><span class="text-blue-400 font-bold">•</span> Mengatur rapat internal OSIS.</li>
            <li class="flex gap-3"><span class="text-blue-400 font-bold">•</span> Menyimpan dokumentasi komunikasi.</li>
          </ul>
        </div>
      </div>

      <!-- Card 2 -->
      <div class="group relative bg-white rounded-3xl p-10 shadow-md border border-slate-200 transition-all hover:shadow-xl hover:-translate-y-1">

        <div class="absolute inset-0 bg-green-200 rounded-3xl opacity-0 group-hover:opacity-20 transition-all"></div>

        <div class="relative z-10 space-y-5">
          <h3 class="text-2xl font-extrabold text-slate-800 flex items-center gap-3">
            <span class="text-3xl">💡</span>
            Tips Koordinasi Efektif
          </h3>

          <div class="space-y-3">
            <div
              v-for="(t, i) in tips"
              :key="i"
              class="flex items-start gap-3 p-3 bg-slate-50 rounded-xl border border-slate-200 hover:border-green-300 hover:bg-green-50 transition-all"
            >
              <span class="text-green-500 text-xl mt-0.5">✔</span>
              <p class="text-slate-700 text-sm">{{ t }}</p>
            </div>
          </div>
        </div>

      </div>

    </div>

  </div>
</template>




<script setup>
const flow = [
  {
    emoji: "🎭",
    title: "Ekstrakurikuler",
    subtitle: "Unit kegiatan siswa",
    bg: "bg-gradient-to-br from-pink-100 to-pink-200"
  },
  {
    emoji: "👥",
    title: "OSIS",
    subtitle: "Pengurus inti & divisi",
    bg: "bg-gradient-to-br from-blue-100 to-blue-200"
  },
  {
    emoji: "👨‍🏫",
    title: "Kesiswaan",
    subtitle: "Wakasek & Pembina",
    bg: "bg-gradient-to-br from-purple-100 to-purple-200"
  }
]

const tips = [
  "Komunikasi jelas dan ringkas.",
  "Patuhi deadline laporan.",
  "Simpan jejak komunikasi.",
  "Pastikan tindak lanjut dilakukan.",
]
</script>




<style scoped>
/* Fade Up */
@keyframes fadeUp {
  from { opacity: 0; transform: translateY(24px); }
  to { opacity: 1; transform: translateY(0); }
}
.animate-fade-up {
  animation: fadeUp 0.6s ease-out forwards;
}

/* Bubble animation */
@keyframes bubble {
  0% { opacity: 0; transform: translateY(24px) scale(0.85); }
  100% { opacity: 1; transform: translateY(0) scale(1); }
}
.animate-bubble {
  animation: bubble 0.6s ease-out forwards;
}
</style>
