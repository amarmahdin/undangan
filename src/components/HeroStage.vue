<script setup>
import Ornament from './Ornament.vue'

defineProps({
  dateLabel: { type: String, default: '' },
  city: { type: String, default: '' },
  showScroll: { type: Boolean, default: false },
})

const floralStyle = {
  backgroundImage: `url(${import.meta.env.BASE_URL}images/floral-line.jpg)`,
  backgroundSize: 'cover',
  backgroundPosition: 'center',
}
</script>

<template>
  <div class="relative flex min-h-dvh w-full flex-col items-center justify-center overflow-hidden bg-burgundy-deep px-6 py-16 text-center text-champagne">
    <div
      class="pointer-events-none absolute inset-0 opacity-[0.16] mix-blend-soft-light"
      
    />
  </div>
</template>