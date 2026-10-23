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

  </article>
</template>