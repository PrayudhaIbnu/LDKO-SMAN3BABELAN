<template>
  <div
    class="bg-white/70 backdrop-blur-xl shadow-md p-6 rounded-2xl border border-gray-200
           transition-all hover:shadow-xl hover:-translate-y-1 text-center">

    <div
      class="w-16 h-16 mx-auto rounded-2xl flex items-center justify-center text-white text-3xl shadow-lg mb-3"
      :class="'bg-' + color + '-500'"
    >
      {{ icon }}
    </div>

    <h3 class="font-bold text-gray-800">{{ title }}</h3>

    <div class="mt-3 text-sm text-gray-600 leading-relaxed">
      <slot />
    </div>

  </div>
</template>

<script setup>
defineProps({
  title: String,
  icon: String,
  color: { type: String, default: 'blue' }
})
</script>
