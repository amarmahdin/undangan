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
      :style="floralStyle"
    />
    <div
      class="pointer-events-none absolute inset-0 bg-gradient-to-b from-burgundy-deep/35 via-transparent to-burgundy-deep/65"
    />
    <div class="relative z-10 flex w-full max-w-lg flex-col items-center">
       <p class="font-display text-[11px] tracking-[0.45em] text-champagne/90 uppercase">
        The Wedding of
      </p>
      <h1 class="mt-6 font-script text-[clamp(3.5rem,13vw,5.75rem)] leading-none text-champagne">
        Euis <span class="text-champagne">&</span> Eka
      </h1>
      
      <Ornament class="mt-6 w-40 text-champagne/70" />

      <p
        v-if="dateLabel"
        class="mt-6 font-display text-sm tracking-[0.22em] text-champagne uppercase sm:text-base"
      >
        {{ dateLabel }}
      </p>
        <p
        v-if="city"
        class="mt-2 font-display text-sm tracking-[0.28em] text-champagne/85 uppercase"
      >
        {{ city }}
      </p>

      
      <slot />
    </div>
  </div>
</template>