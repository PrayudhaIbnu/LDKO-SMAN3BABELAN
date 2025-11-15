<template>
  <div class="flex items-start gap-3 bg-green-50/70 border border-green-200
              rounded-2xl p-3 transition-all hover:shadow-md hover:-translate-y-1">

    <div class="w-7 h-7 bg-green-500 text-white rounded-xl flex items-center justify-center text-sm shadow">
      ✓
    </div>

    <div>
      <p class="font-semibold text-gray-800">{{ title }}</p>
      <p v-if="desc" class="text-xs text-gray-600">{{ desc }}</p>
    </div>

  </div>
</template>

<script setup>
const props = defineProps({ text: String })
const [title, desc] = props.text.split(' — ')
</script>
