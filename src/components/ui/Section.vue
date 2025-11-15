<template>
  <div class="relative pl-4 py-2 group">
    <div :class="'absolute left-0 top-0 h-full w-1 rounded-full bg-gradient-to-b from-' + color + '-400 to-' + color + '-300'"></div>
    <h4 class="font-semibold text-slate-800 group-hover:text-slate-900 transition-colors">{{ title }}</h4>
    <p class="text-sm text-slate-600 leading-relaxed mt-1">{{ text }}</p>
  </div>
</template>

<script setup>
defineProps({
  title: String,
  text: String,
  color: { type: String, default: 'blue' }
})
</script>
