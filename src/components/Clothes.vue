<script setup lang="ts">
</script>

<template>
  <div
    :class="[
    'flex flex-wrap items-start content-start justify-start w-full h-100 ',
    'border-1 border-solid border-black p-2 rounded-md gap-2'
  ]">
    <slot/>
  </div>
</template>

<style>
</style>