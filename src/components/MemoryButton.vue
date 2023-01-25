<template>
  <button class="btn bg-[#637097] text-[#fff] text-base shadow-[0_4px_#404e72]" @click="$emit('updateMemory', value)">
    {{ text }}
  </button>
</template>

<script setup>
const props = defineProps({
  text: {
    required: true,
    type: [String, Number]
  },
  value: {
    required: true,
    type: String
  }
})

</script>

<style scoped>

</style>
