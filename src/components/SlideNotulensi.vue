<template>
  <div class="space-y-10">
    <div class="text-center space-y-3 animate-slide-up">
      <h2 class="text-4xl font-extrabold text-slate-800">📝 Notulensi Rapat</h2>
      <p class="text-slate-600 text-lg font-medium">
        Panduan membuat catatan rapat resmi & rapi
      </p>
    </div>

    <div class="grid md:grid-cols-2 gap-6 max-w-5xl mx-auto">
      <!-- Struktur Notulen -->
      <Card title="Struktur Notulen" icon="📋" color="blue">
        <div class="space-y-4 text-sm">
          <Section
            title="Header"
            text="Hari, tanggal, waktu, tempat, dan agenda rapat."
            color="blue" />
          <Section
            title="Peserta"
            text="Daftar hadir, pimpinan rapat, dan notulis."
            color="green" />
          <Section
            title="Pembahasan"
            text="Poin diskusi dari setiap agenda."
            color="purple" />
          <Section
            title="Keputusan"
            text="Hasil rapat dan tindak lanjut."
            color="orange" />
        </div>
      </Card>

      <!-- Tips -->
      <Card title="Tips Menulis Notulen" icon="💡" color="green">
        <div class="space-y-3">
          <Tip text="Tulis poin penting — Fokus pada hal yang disepakati" />
          <Tip text="Gunakan bahasa formal — Hindari slang" />
          <Tip text="Catat waktu — Jam mulai & selesai" />
          <Tip text="Rapi dan jelas — Gunakan bullet point" />
        </div>
      </Card>
    </div>

    <div
      class="mt-8 bg-gradient-to-r from-blue-50 to-indigo-50 rounded-xl p-6 border border-blue-200">
      <h3 class="text-lg font-bold text-gray-800 mb-3">
        🎯 Contoh Format Singkat
      </h3>
      <div class="bg-white rounded-lg p-4 text-sm font-mono">
        <div class="text-gray-600">
          <strong>NOTULEN RAPAT OSIS</strong><br />
          Hari/Tanggal: Senin, 15 Januari 2024<br />
          Waktu: 14.00 - 16.00 WIB<br />
          Tempat: Ruang OSIS<br /><br /><strong>AGENDA:</strong><br />
          1. Pembahasan kegiatan bulan Februari<br />
          2. Evaluasi kegiatan sebelumnya<br /><br /><strong>KEPUTUSAN:</strong
          ><br />
          - Kegiatan donor darah tanggal 14 Februari<br />
          - PJ: Divisi Kesehatan<br />
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import Card from "@/components/ui/Card.vue";
import Section from "@/components/ui/Section.vue";
import Tip from "@/components/ui/Tip.vue";
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
