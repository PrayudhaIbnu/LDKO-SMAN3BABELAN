<template>
  <div class="space-y-12">
    <!-- HEADER -->
    <div class="text-center space-y-4 animate-fade-up">
      <div class="inline-flex items-center gap-3 px-5 py-2 bg-amber-100 text-amber-700 rounded-full font-semibold shadow-sm border border-amber-200">
        🎯 Quiz Kesekretariatan OSIS
      </div>

      <h2 class="text-4xl font-extrabold text-slate-800 tracking-tight">
        Uji Pemahamanmu!
      </h2>

      <p class="text-slate-600 text-lg max-w-2xl mx-auto leading-relaxed">
        Jawab pertanyaan di bawah untuk mengetahui seberapa baik kamu memahami materi kesekretariatan OSIS.
      </p>
    </div>

    <!-- QUIZ CONTAINER -->
    <div v-if="!isFinished" class="max-w-2xl mx-auto px-6">

      <!-- Progress Bar -->
      <div class="mb-10">
        <div class="flex items-center justify-between mb-3">
          <span class="text-sm font-semibold text-slate-700">
            Pertanyaan {{ currentQuestion + 1 }} dari {{ questions.length }}
          </span>
          <span class="text-xs text-slate-500">{{ Math.round((currentQuestion + 1) / questions.length * 100) }}%</span>
        </div>
        <div class="w-full h-2 bg-slate-200 rounded-full overflow-hidden">
          <div 
            class="h-full bg-gradient-to-r from-amber-400 to-amber-500 rounded-full transition-all duration-500"
            :style="{ width: ((currentQuestion + 1) / questions.length * 100) + '%' }"
          ></div>
        </div>
      </div>

      <!-- QUESTION CARD -->
      <div class="bg-white rounded-2xl border-2 border-slate-200 p-10 shadow-lg hover:shadow-xl transition-shadow animate-fade-up">

        <!-- Question Number Badge -->
        <div class="inline-flex items-center justify-center w-12 h-12 rounded-full bg-gradient-to-br from-amber-400 to-amber-500 text-white font-bold text-lg shadow-md ring-4 ring-amber-100 mb-6">
          {{ currentQuestion + 1 }}
        </div>

        <!-- Question Text -->
        <h3 class="text-2xl font-bold text-slate-800 mb-8 leading-relaxed">
          {{ questions[currentQuestion].question }}
        </h3>

        <!-- Answer Options -->
        <div class="space-y-3 mb-10">
          <button
            v-for="(option, idx) in questions[currentQuestion].options"
            :key="idx"
            @click="selectAnswer(idx)"
            :class="[
              'w-full text-left p-5 rounded-xl border-2 transition-all duration-200 font-medium text-slate-700',
              selectedAnswer === idx
                ? 'bg-amber-100 border-amber-500 text-slate-800'
                : 'bg-slate-50 border-slate-200 hover:border-slate-300 hover:bg-slate-100'
            ]"
          >
            <div class="flex items-center gap-4">
              <div 
                :class="[
                  'w-6 h-6 rounded-full border-2 flex items-center justify-center flex-shrink-0 transition-all',
                  selectedAnswer === idx
                    ? 'bg-amber-500 border-amber-500'
                    : 'border-slate-300'
                ]"
              >
                <span v-if="selectedAnswer === idx" class="text-white text-sm font-bold">✓</span>
              </div>
              <span>{{ option }}</span>
            </div>
          </button>
        </div>

        <!-- Action Buttons -->
        <div class="flex gap-4 justify-between">
          <button
            @click="previousQuestion"
            :disabled="currentQuestion === 0"
            class="px-6 py-3 rounded-xl border-2 border-slate-300 bg-white text-slate-700 font-semibold
                   shadow-sm hover:shadow-md hover:border-slate-400 disabled:opacity-50 disabled:cursor-not-allowed
                   transition-all hover:-translate-y-1 duration-200"
          >
            ← Sebelumnya
          </button>

          <button
            @click="nextQuestion"
            :disabled="selectedAnswer === null"
            class="px-8 py-3 rounded-xl bg-gradient-to-r from-amber-500 to-amber-600 text-white font-semibold
                   shadow-lg hover:shadow-xl disabled:opacity-50 disabled:cursor-not-allowed
                   transition-all hover:-translate-y-1 duration-200"
          >
            {{ currentQuestion === questions.length - 1 ? 'Selesai' : 'Lanjut' }} →
          </button>
        </div>

      </div>

    </div>

    <!-- RESULTS SCREEN -->
    <div v-else class="max-w-2xl mx-auto px-6 animate-fade-up">

      <!-- Score Card -->
      <div class="bg-white rounded-2xl border-2 border-slate-200 p-12 shadow-lg text-center">

        <!-- Trophy Icon -->
        <div class="text-7xl mb-6 animate-bounce">
          {{ score >= 80 ? '🏆' : score >= 60 ? '⭐' : '📚' }}
        </div>

        <!-- Score Display -->
        <h2 class="text-4xl font-extrabold text-slate-800 mb-2">
          {{ score }}%
        </h2>

        <!-- Message -->
        <p class="text-xl text-slate-600 mb-8 leading-relaxed">
          {{ scoreMessage }}
        </p>

        <!-- Score Breakdown -->
        <div class="bg-slate-50 rounded-xl p-6 mb-8 text-left space-y-3">
          <div class="flex justify-between items-center">
            <span class="text-slate-700 font-semibold">Jawaban Benar</span>
            <span class="text-green-600 font-bold text-lg">{{ correctAnswers }}/{{ questions.length }}</span>
          </div>
          <div class="w-full h-2 bg-slate-200 rounded-full overflow-hidden">
            <div 
              class="h-full bg-gradient-to-r from-green-400 to-green-500 rounded-full transition-all"
              :style="{ width: (correctAnswers / questions.length * 100) + '%' }"
            ></div>
          </div>
        </div>

        <!-- Detailed Results -->
        <div class="space-y-3 mb-10 max-h-80 overflow-y-auto">
          <div
            v-for="(q, idx) in questions"
            :key="idx"
            :class="[
              'p-4 rounded-lg border-2 text-left transition-all',
              userAnswers[idx] === q.correct
                ? 'bg-green-50 border-green-200'
                : 'bg-red-50 border-red-200'
            ]"
          >
            <div class="flex gap-3 items-start mb-2">
              <span :class="[
                'w-6 h-6 rounded-full flex items-center justify-center flex-shrink-0 font-bold text-sm text-white',
                userAnswers[idx] === q.correct ? 'bg-green-500' : 'bg-red-500'
              ]">
                {{ userAnswers[idx] === q.correct ? '✓' : '✗' }}
              </span>
              <div class="flex-1">
                <p class="font-semibold text-slate-800 text-sm mb-1">{{ q.question }}</p>
                <p class="text-xs text-slate-600">
                  <span class="font-semibold">Jawaban Kamu:</span> {{ q.options[userAnswers[idx]] }}
                </p>
                <p v-if="userAnswers[idx] !== q.correct" class="text-xs text-green-700 font-semibold mt-1">
                  <span>Jawaban Benar:</span> {{ q.options[q.correct] }}
                </p>
              </div>
            </div>
          </div>
        </div>

        <!-- Action Buttons -->
        <div class="flex gap-4 justify-center">
          <button
            @click="resetQuiz"
            class="px-8 py-3 rounded-xl bg-gradient-to-r from-slate-600 to-slate-700 text-white font-semibold
                   shadow-lg hover:shadow-xl transition-all hover:-translate-y-1 duration-200"
          >
            🔄 Ulangi Quiz
          </button>
        </div>

      </div>

    </div>

    <!-- Bottom Spacing -->
    <div class="h-8"></div>

  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const questions = ref([
  {
    question: "Apa fungsi utama surat masuk dalam kesekretariatan OSIS?",
    options: [
      "Mencatat semua komunikasi dari pihak luar ke OSIS",
      "Mengirim informasi ke sekolah",
      "Menyimpan data siswa",
      "Membuat laporan bulanan"
    ],
    correct: 0
  },
  {
    question: "Dalam alur birokrasi perizinan kegiatan, siapa yang menyahkan proposal setelah pembina OSIS?",
    options: [
      "Wakil Kepala Sekolah",
      "Kepala Sekolah",
      "Guru Pembina OSIS",
      "Ketua OSIS"
    ],
    correct: 1
  },
  {
    question: "Apa itu notulensi rapat?",
    options: [
      "Daftar peserta rapat",
      "Catatan resmi berisi rangkuman pembahasan, keputusan, dan tindak lanjut",
      "Jadwal rapat bulanan",
      "Anggaran biaya kegiatan"
    ],
    correct: 1
  },
  {
    question: "Komponen apa yang HARUS ada dalam sebuah proposal kegiatan OSIS?",
    options: [
      "Hanya tujuan dan tanggal",
      "Latar belakang, tujuan, rundown, anggaran, dan struktur panitia",
      "Hanya nama peserta",
      "Hanya foto-foto acara"
    ],
    correct: 1
  },
  {
    question: "Siapa yang bertanggung jawab dalam koordinasi komunikasi antara OSIS dengan pihak sekolah?",
    options: [
      "Sekretaris OSIS",
      "Koordinator Komunikasi/Hubungan Eksternal",
      "Bendahara OSIS",
      "Ketua Divisi Acara"
    ],
    correct: 1
  },
  {
    question: "Apa manfaat dari kearsipan dokumentasi OSIS yang baik?",
    options: [
      "Hanya untuk koleksi pribadi",
      "Referensi sejarah organisasi, bukti pertanggungjawaban, dan acuan kebijakan",
      "Tidak ada manfaat khusus",
      "Hanya untuk laporan akhir tahun"
    ],
    correct: 1
  }
])

const currentQuestion = ref(0)
const selectedAnswer = ref(null)
const userAnswers = ref([])
const isFinished = ref(false)

const correctAnswers = computed(() => {
  return userAnswers.value.filter((ans, idx) => ans === questions.value[idx].correct).length
})

const score = computed(() => {
  return Math.round((correctAnswers.value / questions.value.length) * 100)
})

const scoreMessage = computed(() => {
  if (score.value >= 80) {
    return "Luar biasa! Kamu memahami materi dengan sangat baik! 🎉"
  } else if (score.value >= 60) {
    return "Bagus! Kamu sudah memahami materi dengan cukup baik. 👍"
  } else {
    return "Jangan menyerah! Coba pelajari kembali materi yang belum dipahami. 💪"
  }
})

function selectAnswer(idx) {
  selectedAnswer.value = idx
}

function nextQuestion() {
  if (selectedAnswer.value !== null) {
    userAnswers.value[currentQuestion.value] = selectedAnswer.value
    
    if (currentQuestion.value < questions.value.length - 1) {
      currentQuestion.value++
      selectedAnswer.value = userAnswers.value[currentQuestion.value] ?? null
    } else {
      isFinished.value = true
    }
  }
}

function previousQuestion() {
  if (currentQuestion.value > 0) {
    userAnswers.value[currentQuestion.value] = selectedAnswer.value
    currentQuestion.value--
    selectedAnswer.value = userAnswers.value[currentQuestion.value] ?? null
  }
}

function resetQuiz() {
  currentQuestion.value = 0
  selectedAnswer.value = null
  userAnswers.value = []
  isFinished.value = false
}
</script>

<style scoped>
@keyframes fadeUp {
  from { 
    opacity: 0; 
    transform: translateY(26px); 
  }
  to { 
    opacity: 1; 
    transform: translateY(0); 
  }
}

.animate-fade-up {
  animation: fadeUp 0.6s ease-out forwards;
}

@keyframes bounce {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px);
  }
}

.animate-bounce {
  animation: bounce 1s ease-in-out infinite;
}
</style>