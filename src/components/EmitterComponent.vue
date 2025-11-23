<script setup>

// declare emitted events
const emit = defineEmits(['response'])

// emit with argument
emit('response', 'hello from child')
</script>

<template>
  <h3>Emitter Component</h3>
  <p>This is a placeholder for EmitterComponent.vue</p>

</template>

<style scoped>
</style>
