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

  <path
      d="M52 40c8-14 28-16 36-4 6 9 2 20-6 26-10 8-24 6-30-2-5-7-4-15 0-20Z"
      fill="#8b3a45"
      opacity="0.55"
    />
    <path
      d="M58 46c6-10 20-12 26-3 4 7 1 15-5 19-8 6-18 4-22-2-3-5-2-11 1-14Z"
      fill="#c4a08a"
      opacity="0.7"
    />
    <path
      d="M66 52c3-6 11-7 14-2 2 4 0 8-3 10-4 3-9 2-11-1-2-3-1-5 0-7Z"
      
    />
  </svg>
</template>