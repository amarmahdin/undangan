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
      fill="#f3e6d4"
      opacity="0.75"
    />

     <path
      d="M96 62c12-10 30-6 34 8 3 12-4 24-16 28-14 5-28-2-32-14-3-10 3-18 14-22Z"
      fill="#4a1520"
      opacity="0.5"
    />
     <path
      d="M102 70c8-7 20-4 22 5 2 8-3 16-11 18-9 3-18-2-20-10-2-6 2-11 9-13Z"
      fill="#6b2a36"
      opacity="0.65"
    />

    <!-- leaves -->
    <path
      d="M40 110c18-8 34 2 38 18-16 4-30-2-38-18Z"
      fill="#5c6b4a"
      opacity="0.35"
    />
    <path
      d="M28 86c14 10 16 28 6 40-12-12-16-28-6-40Z"
      fill="#4a5c3a"
      opacity="0.3"
    />
    <path
      d="M118 96c16 6 22 22 14 36-14-8-22-22-14-36Z"
      fill="#5c6b4a"
      opacity="0.28"
    />

    <!-- small buds -->
    <circle cx="34" cy="64" r="5" fill="#a67c3d" opacity="0.45" />
    <circle cx="128" cy="118" r="4" fill="#8b3a45" opacity="0.4" />
    <circle cx="22" cy="118" r="3.5" fill="#c9a36a" opacity="0.4" />

     <!-- fine stem lines -->
    <path
      d="M48 118c8 22 6 48-4 72"
      stroke="#6e4d52"
      stroke-width="1.2"
      opacity="0.35"
    />
    <path
      d="M92 118c4 20 2 44-6 66"
      stroke="#6e4d52"
      stroke-width="1"
      opacity="0.28"
    />
  </svg>
</template>