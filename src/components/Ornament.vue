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
    <path
      d="M50 12c4-8 16-8 20 0-4 8-16 8-20 0Z"
      stroke="currentColor"
      stroke-width="1"
      fill="none"
    />
    <circle cx="60" cy="12" r="2.2" fill="currentColor" />
</template>