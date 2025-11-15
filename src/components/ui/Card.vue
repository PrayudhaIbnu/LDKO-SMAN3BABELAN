<template>
  <div
    class="bg-white rounded-2xl p-6 shadow-md border border-gray-200
           transition-all hover:shadow-lg hover:-translate-y-1 cursor-pointer">
    
    <div class="flex items-center mb-4 gap-3">
      <div
        class="w-12 h-12 rounded-xl flex items-center justify-center text-white text-xl 
               shadow-md transition-all group-hover:scale-110"
        :class="'bg-gradient-to-br from-' + color + '-400 to-' + color + '-600'"
      >
        {{ icon }}
      </div>

      <h3 class="text-xl font-bold text-slate-800">
        {{ title }}
      </h3>
    </div>

    <div>
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
