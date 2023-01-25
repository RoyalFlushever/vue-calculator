<template>
  <button class="btn bg-[#eae3dc] text-[#444b5a] text-[2rem] shadow-[0_4px_#b4a597]" @click="$emit('updateScreen', value)">
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
