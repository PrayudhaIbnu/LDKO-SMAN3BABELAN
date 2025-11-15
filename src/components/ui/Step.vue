<template>
  <div class="relative animate-slide-up" :style="{ animationDelay: delay + 's' }">
    <!-- Connecting Line Background -->
    <div v-if="!isLast" class="absolute left-6 top-24 w-0.5 h-24 bg-gradient-to-b from-blue-400 via-blue-300 to-transparent"></div>

    <!-- Step Card -->
    <div class="relative flex gap-6 items-start">
      <!-- Number Badge with Glow -->
      <div class="relative flex-shrink-0 z-10">
        <div class="absolute inset-0 w-12 h-12 bg-blue-400 rounded-full blur-lg opacity-40"></div>
        <div class="relative w-12 h-12 rounded-full bg-gradient-to-br from-blue-500 to-blue-600 text-white flex items-center justify-center font-bold text-lg shadow-lg ring-4 ring-blue-100 hover:scale-110 transition-transform duration-300">
          {{ number }}
        </div>
      </div>

      <!-- Content Card -->
      <div class="flex-1 pt-1 pb-6">
        <div class="bg-white border-2 border-slate-200 rounded-xl p-5 shadow-sm hover:shadow-md hover:border-blue-300 transition-all duration-300 group">
          <h3 class="text-lg font-bold text-slate-800 mb-2 group-hover:text-blue-600 transition-colors">{{ title }}</h3>
          <p class="text-slate-600 text-sm leading-relaxed">{{ desc }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
defineProps({
  number: { type: Number, required: true },
  title: { type: String, required: true },
  desc: { type: String, required: true },
  delay: { type: Number, default: 0 },
  isLast: { type: Boolean, default: false }
})
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