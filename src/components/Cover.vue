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
      <p class="font-display text-[11px] tracking-[0.45em] text-champagne/90 uppercase">
        The Wedding of
      </p>
    </div>
    <div class="flex flex-col items-center animate-fade-up-delay">
      <h1 class="font-script text-[clamp(3.5rem,13vw,5.75rem)] leading-none text-champagne">
        Euis <span class="text-champagne">&</span> Eka
      </h1>
      <Ornament class="mt-6 w-40 text-champagne/70" />
      <p class="mt-6 font-display text-sm tracking-[0.22em] text-champagne uppercase sm:text-base">
        Senin, 19 Oktober 2026
      </p>
      <p class="mt-2 font-display text-sm tracking-[0.28em] text-champagne/85 uppercase">
        Kota Baubau
      </p>
    </div>

    <div
        class="flex w-full flex-col items-center gap-5 pb-[max(0.5rem,env(safe-area-inset-bottom))] animate-fade-up-delay-2"
      >

    </div>
    </div>
  </section>>
</template>