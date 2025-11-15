<template>
  <div class="space-y-10">

    <div class="text-center space-y-3 animate-slide-up">
      <h2 class="text-4xl font-extrabold text-slate-800">🤝 Koordinasi Struktur OSIS</h2>
      <p class="text-slate-600 text-lg font-medium">Memahami alur komunikasi dalam organisasi sekolah</p>
    </div>

    <!-- Vertical flow -->
    <div class="flex flex-col items-center space-y-6">

      <Box emoji="🎭" title="Ekstrakurikuler" subtitle="Unit kegiatan siswa" color="blue" />
      <Arrow />

      <Box emoji="👥" title="OSIS" subtitle="Pengurus inti & divisi" color="green" />
      <Arrow />

      <Box emoji="👨‍🏫" title="Kesiswaan" subtitle="Wakasek & Pembina" color="purple" />
    </div>

    <!-- 2 columns -->
    <div class="grid md:grid-cols-2 gap-6 max-w-5xl mx-auto">

      <Card title="Tugas Koordinasi" icon="📋" color="blue">
        <ul class="text-sm text-slate-700 leading-relaxed">
          <li class="flex items-start gap-2"><span>•</span> <span>Menyampaikan informasi resmi ke ekstrakurikuler.</span></li>
          <li class="flex items-start gap-2"><span>•</span> <span>Melaporkan kegiatan OSIS ke pembina.</span></li>
          <li class="flex items-start gap-2"><span>•</span> <span>Mengatur rapat internal OSIS.</span></li>
          <li class="flex items-start gap-2"><span>•</span> <span>Menyimpan dokumentasi komunikasi.</span></li>
        </ul>
      </Card>

      <Card title="Tips Koordinasi Efektif" icon="💡" color="green">
        <div class="space-y-3">
          <Tip text="Komunikasi jelas — Sampaikan informasi dengan ringkas" />
          <Tip text="Tepat waktu — Penuhi deadline laporan" />
          <Tip text="Dokumentasi — Simpan arsip komunikasi" />
          <Tip text="Follow up — Pastikan tindak lanjut dikerjakan" />
        </div>
      </Card>

    </div>

  </div>
</template>

<script setup>
import Box from '@/components/ui/Box.vue'
import Arrow from '@/components/ui/Arrow.vue'
import Card from '@/components/ui/Card.vue'
import Tip from '@/components/ui/Tip.vue'
</script>

<style scoped>
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
</style>