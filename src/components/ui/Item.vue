<template>
  <div class="relative pl-4 py-2 group">
    <div :class="'absolute left-0 top-0 h-full w-1 bg-gradient-to-b from-' + color + '-400 to-' + color + '-300 rounded-full'"></div>

    <h4 class="font-semibold text-slate-800 group-hover:text-slate-900 transition-colors">
      {{ no }}. {{ title }}
    </h4>

    <p class="text-sm text-slate-600 mt-1 leading-relaxed">
      {{ text }}
    </p>
  </div>
</template>

<script setup>
defineProps({
  no: Number,
  title: String,
  text: String,
  color: { type: String, default: 'blue' }
})
</script>
