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
      <div v-if="showScroll" class="mt-12 flex flex-col items-center gap-2">
        <span
          class="flex h-9 w-5 items-start justify-center rounded-full border border-champagne/45 pt-1.5"
          aria-hidden="true"
        >
          <span class="scroll-dot h-1.5 w-1.5 rounded-full bg-champagne" />
        </span>
      </div>
      <slot />
    </div>
  </div>
</template>

<style scoped>
.scroll-dot {
  animation: scroll-bounce 1.6s ease-in-out infinite;
}

@keyframes scroll-bounce {
  0%,
  100% {
    transform: translateY(0);
    opacity: 0.7;
  }
  50% {
    transform: translateY(8px);
    opacity: 1;
  }
}


</style>