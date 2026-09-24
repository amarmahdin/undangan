<script setup>
defineProps({
  className: { type: String, default: 'text-gold' },
})
</script>

<template>
<svg
    :class="className"
    viewBox="0 0 120 24"
    fill="none"
    xmlns="http://www.w3.org/2000/svg"
    aria-hidden="true"
  >
  <path
      d="M4 12h32M84 12h32"
      stroke="currentColor"
      stroke-width="1"
      stroke-linecap="round"
    />
</template>