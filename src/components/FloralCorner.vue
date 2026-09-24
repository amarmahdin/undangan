<script setup>
defineProps({
  side: { type: String, default: 'left' }, // left | right
})
</script>

<template>
<svg
    viewBox="0 0 200 240"
    fill="none"
    xmlns="http://www.w3.org/2000/svg"
    aria-hidden="true"
    class="pointer-events-none h-auto w-full"
    :class="side === 'right' ? '-scale-x-100' : ''"
  >
  
  </svg>
</template>