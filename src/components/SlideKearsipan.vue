<template>
  <div class="space-y-16">

    <!-- HEADER -->
    <div class="text-center space-y-4 animate-fade-up">
      <div class="inline-flex items-center gap-3 px-5 py-2 bg-blue-50 text-blue-700 rounded-full font-semibold shadow-sm border border-blue-200">
        🗂️ Kearsipan OSIS
      </div>

      <h2 class="text-4xl font-extrabold text-slate-800 tracking-tight">
        Sistem Kearsipan yang Tertib & Profesional
      </h2>

      <p class="text-slate-600 text-lg max-w-2xl mx-auto">
        Pengelolaan dokumen OSIS secara rapi, efisien, dan mudah ditelusuri kapan saja.
      </p>
    </div>


    <!-- 3 BLOCK INFORMATION -->
    <div class="max-w-6xl mx-auto grid md:grid-cols-3 gap-8 px-4">

      <div
        v-for="box in infoBlocks"
        :key="box.title"
        class="group bg-white rounded-2xl shadow-md p-7 border border-slate-200 transition-all hover:shadow-xl hover:-translate-y-1 relative overflow-hidden"
      >
        <!-- Glow -->
        <div
          class="absolute inset-0 opacity-0 group-hover:opacity-20 transition-all duration-300"
          :class="box.glow"
        ></div>

        <div class="relative z-10 flex flex-col items-center text-center space-y-3">
          <div class="text-5xl">{{ box.icon }}</div>

          <h3 class="text-xl font-bold text-slate-800 tracking-wide">
            {{ box.title }}
          </h3>

          <p class="text-slate-600 text-sm leading-relaxed">
            {{ box.desc }}
          </p>
        </div>
      </div>

    </div>

    <hr>

    <!-- STEPS CARD -->
    <div class="max-w-5xl mx-auto bg-white rounded-3xl shadow-md border border-slate-200 p-10 space-y-10 animate-fade-up">

      <div class="text-center space-y-2">
        <h3 class="text-2xl font-extrabold text-slate-800">📋 Langkah Kearsipan</h3>
        <p class="text-slate-500 text-sm">Ikuti alur berikut untuk memastikan arsip tersimpan rapi</p>
      </div>

      <div class="grid md:grid-cols-4 gap-8">

        <div
          v-for="(step, idx) in steps"
          :key="idx"
          class="flex flex-col items-center text-center space-y-4 animate-step-fade"
          :style="{ animationDelay: (idx * 0.1) + 's' }"
        >
          <!-- Number -->
          <div
            class="w-16 h-16 flex items-center justify-center text-2xl font-extrabold text-white rounded-full shadow-lg ring-4 ring-white"
            :class="step.color"
          >
            {{ step.number }}
          </div>

          <!-- Title -->
          <h4 class="text-base font-bold text-slate-800">
            {{ step.title }}
          </h4>

          <!-- Desc -->
          <p class="text-slate-600 text-xs leading-relaxed max-w-[140px]">
            {{ step.text }}
          </p>
        </div>

      </div>
     <div class="mt-8 bg-gradient-to-r from-red-50 to-pink-50 rounded-xl p-6 border border-red-200">
      <h3 class="text-lg font-bold text-gray-800 mb-4 flex items-center"><span class="text-2xl mr-3">⚠️</span> Hal yang Perlu Diperhatikan</h3>
      <div class="grid md:grid-cols-2 gap-4 text-sm">
       <div class="space-y-2">
        <div class="flex items-start space-x-2"><span class="text-red-500 mt-1">•</span> <span>Jaga kerahasiaan dokumen penting</span>
        </div>
        <div class="flex items-start space-x-2"><span class="text-red-500 mt-1">•</span> <span>Backup dokumen digital secara berkala</span>
        </div>
        <div class="flex items-start space-x-2"><span class="text-red-500 mt-1">•</span> <span>Hindari menumpuk dokumen</span>
        </div>
       </div>
       <div class="space-y-2">
        <div class="flex items-start space-x-2"><span class="text-red-500 mt-1">•</span> <span>Periksa kondisi fisik dokumen</span>
        </div>
        <div class="flex items-start space-x-2"><span class="text-red-500 mt-1">•</span> <span>Buat daftar arsip yang mudah dicari</span>
        </div>
        <div class="flex items-start space-x-2"><span class="text-red-500 mt-1">•</span> <span>Serahkan arsip saat pergantian pengurus</span>
        </div>
       </div>
      </div>
     </div>
    </div>

  </div>
</template>



<script setup>
const infoBlocks = [
  {
    title: "Klasifikasi",
    icon: "📁",
    desc: "Surat masuk/keluar, proposal, LPJ, notulen.",
    glow: "bg-blue-300"
  },
  {
    title: "Kronologis",
    icon: "📅",
    desc: "Dokumen diurut berdasarkan tahun dan tanggal kegiatan.",
    glow: "bg-green-300"
  },
  {
    title: "Kode Arsip",
    icon: "🏷️",
    desc: "SM (Surat Masuk), SK (Surat Keluar), PR (Proposal), NT (Notulen).",
    glow: "bg-purple-300"
  }
]

const steps = [
  {
    number: "1",
    title: "Terima Dokumen",
    text: "Catat tanggal & nomor dokumen.",
    color: "bg-blue-600"
  },
  {
    number: "2",
    title: "Klasifikasi",
    text: "Tentukan kategori dokumen.",
    color: "bg-green-600"
  },
  {
    number: "3",
    title: "Simpan",
    text: "Letakkan di map/lemari sesuai kode.",
    color: "bg-purple-600"
  },
  {
    number: "4",
    title: "Catat Arsip",
    text: "Update daftar arsip berkala.",
    color: "bg-orange-500"
  }
]
</script>



<style scoped>
/* Fade Up */
@keyframes fadeUp {
  from { opacity: 0; transform: translateY(26px); }
  to { opacity: 1; transform: translateY(0); }
}
.animate-fade-up {
  animation: fadeUp 0.6s ease-out forwards;
}

/* Step Fade */
@keyframes stepFade {
  from { opacity: 0; transform: translateY(18px); }
  to { opacity: 1; transform: translateY(0); }
}
.animate-step-fade {
  animation: stepFade 0.5s ease-out forwards;
}
</style>
