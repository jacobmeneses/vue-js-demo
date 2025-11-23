<script setup>
import { ref } from 'vue'

const clsOne = ref('text-orange-500');

</script>

<template>
  <div>
    <h1 :class="clsOne">You did it!</h1>

    <p>
      Visit <a href="https://vuejs.org/" target="_blank" rel="noopener">vuejs.org</a> to read the
      documentation
    </p>
  </div>
</template>

<style>
</style>
