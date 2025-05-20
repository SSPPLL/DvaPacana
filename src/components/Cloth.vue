<script setup lang="ts">
defineProps<{
  name: string
}>()
</script>

<template>
  <button :class="[
    'border-1 border-solid border-black p-2 rounded-md leading-normal cursor-pointer appearance-none outline-none',
  ]">
    {{ name }}
  </button>
</template>

<style>
</style>