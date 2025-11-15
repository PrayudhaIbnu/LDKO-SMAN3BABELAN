<template>
  <div class="space-y-10">

    <div class="text-center space-y-3 animate-slide-up">
      <h2 class="text-4xl font-extrabold text-slate-800">✉️ Surat Menyurat</h2>
      <p class="text-slate-600 text-lg font-medium">Jenis & format surat resmi dalam organisasi OSIS</p>
    </div>

    <div class="grid md:grid-cols-2 gap-6 max-w-5xl mx-auto">

      <Card title="Surat Undangan" icon="📨" color="blue">
        <ul class="text-sm leading-relaxed text-slate-700">
          <li class="flex items-start gap-2"><span>•</span> <span>Kop surat</span></li>
          <li class="flex items-start gap-2"><span>•</span> <span>Nomor surat</span></li>
          <li class="flex items-start gap-2"><span>•</span> <span>Perihal</span></li>
          <li class="flex items-start gap-2"><span>•</span> <span>Isi undangan</span></li>
          <li class="flex items-start gap-2"><span>•</span> <span>Penutup & tanda tangan</span></li>
        </ul>
      </Card>

      <Card title="Surat Keluar / Masuk" icon="📤" color="green">
        <div class="space-y-3 text-sm">
          <div class="bg-blue-50 rounded-xl p-4 border border-blue-200">
            <b class="text-slate-800">Surat Masuk:</b><br>
            <span class="text-slate-700">Dicatat, diberi disposisi, lalu diarsipkan.</span>
          </div>
          <div class="bg-green-50 rounded-xl p-4 border border-green-200">
            <b class="text-slate-800">Surat Keluar:</b><br>
            <span class="text-slate-700">Dibuat nomor surat, ekspedisi, dan tembusan arsip.</span>
          </div>
        </div>
      </Card>

      <Card title="Surat Peminjaman Barang" icon="📦" color="purple">
        <ul class="text-sm text-slate-700 leading-relaxed">
          <li class="flex items-start gap-2"><span>•</span> <span>Identitas peminjam</span></li>
          <li class="flex items-start gap-2"><span>•</span> <span>Daftar barang</span></li>
          <li class="flex items-start gap-2"><span>•</span> <span>Durasi penggunaan</span></li>
          <li class="flex items-start gap-2"><span>•</span> <span>Tanda tangan peminjam</span></li>
        </ul>
      </Card>

      <Card title="Surat Peminjaman Ruangan" icon="🏢" color="orange">
        <ul class="text-sm leading-relaxed text-slate-700">
          <li class="flex items-start gap-2"><span>•</span> <span>Ruangan yang digunakan</span></li>
          <li class="flex items-start gap-2"><span>•</span> <span>Keperluan kegiatan</span></li>
          <li class="flex items-start gap-2"><span>•</span> <span>Jumlah peserta</span></li>
          <li class="flex items-start gap-2"><span>•</span> <span>Penanggung jawab</span></li>
        </ul>
      </Card>

    </div>

  </div>
</template>

<script setup>
import Card from '@/components/ui/Card.vue'
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