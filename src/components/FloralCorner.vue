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
  <ellipse cx="48" cy="52" rx="42" ry="38" fill="#6b2a36" opacity="0.18" />
  <ellipse cx="88" cy="78" rx="36" ry="32" fill="#c9a36a" opacity="0.16" />
  <ellipse cx="56" cy="98" rx="28" ry="24" fill="#a67c3d" opacity="0.12" />
  </svg>
</template>