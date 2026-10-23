<script setup>
defineProps({
  title: { type: String, required: true },
  dayName: { type: String, required: true },
  day: { type: String, required: true },
  monthYear: { type: String, required: true },
  time: { type: String, required: true },
  venueAddress: { type: String, required: true },
  mapsLink: { type: String, required: true },
})
</script>

<template>
  <article class="event-oval relative mx-auto flex w-full max-w-[340px] flex-col items-center px-8 py-12 text-center sm:px-10 sm:py-14">
  
    <div class="event-floral pointer-events-none absolute inset-0" aria-hidden="true" />

    <h4 class="relative z-[1] font-display text-xl tracking-[0.28em] text-burgundy uppercase">
      {{ title }}
    </h4>

    <div class="relative z-[1] mx-auto mt-3 h-px w-16 bg-gold/60" />
    <p class="relative z-[1] mt-6 font-script text-3xl text-ink">{{ dayName }}</p>
    <p class="relative z-[1] mt-1 font-display text-6xl font-semibold leading-none text-burgundy">
      {{ day }}
    </p>
    <p class="relative z-[1] mt-2 font-display text-sm tracking-[0.18em] text-ink uppercase">
      {{ monthYear }}
    </p>
    
    <p class="relative z-[1] mt-6 inline-flex items-center gap-2 font-display text-sm text-burgundy">
      <span
        class="inline-flex h-6 w-6 items-center justify-center rounded-full bg-burgundy text-[10px] text-champagne"
        aria-hidden="true"
      >
        ◷
      </span>
      {{ time }}
    </p>

    <div class="relative z-[1] mt-8">
      <p class="font-display text-sm tracking-[0.12em] text-burgundy">Lokasi Acara</p>
      <p class="mt-2 font-display text-lg text-ink">{{ venueName }}</p>
      <p class="mx-auto mt-1 max-w-[220px] text-sm leading-relaxed text-muted">
        {{ venueAddress }}
      </p>
    </div>

    <a
      :href="mapsLink"
      target="_blank"
      rel="noopener noreferrer"
      class="relative z-[1] mt-8 inline-flex min-h-11 cursor-pointer items-center justify-center gap-2 rounded-full bg-burgundy px-7 py-2.5 text-sm font-medium tracking-wide text-champagne shadow-[0_10px_24px_rgba(74,21,32,0.25)] transition duration-200 hover:bg-burgundy-soft focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-4 focus-visible:outline-burgundy"
      >
      <svg class="h-4 w-4" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true">
        
      </svg>
    </a>
  </article>
</template>