<template>
  <div
    class="rounded-2xl p-4 w-48 text-center shadow-md border transition-all
           hover:shadow-xl hover:-translate-y-1 cursor-pointer"
    :class="'bg-' + color + '-100/80 border-' + color + '-300'"
  >
    <div class="text-3xl mb-2">{{ emoji }}</div>
    <h4 :class="'font-bold text-' + color + '-800'">{{ title }}</h4>
    <p :class="'text-sm text-' + color + '-600'">{{ subtitle }}</p>
  </div>
</template>

<script setup>
defineProps({
  emoji: String,
  title: String,
  subtitle: String,
  color: { type: String, default: 'blue' }
})
</script>
