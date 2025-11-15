<template>
  <div class="space-y-10">

    <div class="text-center space-y-3 animate-slide-up">
      <h2 class="text-4xl font-extrabold text-slate-800">📊 Proposal & LPJ</h2>
      <p class="text-slate-600 text-lg font-medium">Format resmi penyusunan proposal & laporan kegiatan OSIS</p>
    </div>

    <div class="grid md:grid-cols-2 gap-6 max-w-5xl mx-auto">

      <!-- Proposal -->
      <Card title="Proposal Kegiatan" icon="📘" color="blue">
        <div class="space-y-4 text-sm text-slate-700">
          <Item no="1" color="blue" title="Latar Belakang" text="Alasan kegiatan diperlukan." />
          <Item no="2" color="green" title="Tujuan" text="Apa yang ingin dicapai." />
          <Item no="3" color="purple" title="Rundown" text="Urutan acara kegiatan." />
          <Item no="4" color="orange" title="Anggaran" text="Rincian biaya kegiatan." />
        </div>
      </Card>

      <!-- LPJ -->
      <Card title="Laporan Pertanggungjawaban (LPJ)" icon="📈" color="green">
        <div class="space-y-4 text-sm text-slate-700">
          <Item no="1" color="blue" title="Pendahuluan" text="Ringkasan kegiatan." />
          <Item no="2" color="green" title="Pelaksanaan" text="Detail kegiatan berjalan." />
          <Item no="3" color="purple" title="Keuangan" text="Pemasukan & pengeluaran." />
          <Item no="4" color="orange" title="Evaluasi" text="Kelebihan & kekurangan kegiatan." />
        </div>
      </Card>

    </div>

  </div>
</template>

<script setup>
import Card from '@/components/ui/Card.vue'
import Item from '@/components/ui/Item.vue'
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