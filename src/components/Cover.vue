<script setup>
import Ornament from './Ornament.vue'

defineProps({
  guestName: { type: String, required: true },
  visible: { type: Boolean, default: true },
})

defineEmits(['open'])

const floralStyle = {
  backgroundImage: `url(${import.meta.env.BASE_URL}images/floral-line.jpg)`,
  backgroundSize: 'cover',
  backgroundPosition: 'center',
}
</script>

<template>  
  <section
    :class="visible ? 'translate-y-0 opacity-100' : '-translate-y-full opacity-0 pointer-events-none'"
    class="fixed inset-0 z-50 flex items-center justify-center overflow-hidden bg-burgundy-deep transition-[transform,opacity] duration-700 ease-[cubic-bezier(0.22,1,0.36,1)]"
    :aria-hidden="!visible"
  > 
  <div
      class="pointer-events-none absolute inset-0 opacity-[0.16] mix-blend-soft-light"
      :style="floralStyle"
    />
  <div
      class="pointer-events-none absolute inset-0 bg-gradient-to-b from-burgundy-deep/40 via-transparent to-burgundy-deep/70"
    />

    <div
      class="relative z-10 flex min-h-dvh w-full max-w-lg flex-col items-center justify-between px-6 py-10 text-center text-champagne sm:px-10"
    >
    <div class="flex flex-col items-center animate-fade-up pt-4">
        
    </div>
  </section>>
</template>