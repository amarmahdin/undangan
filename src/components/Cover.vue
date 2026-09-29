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
      <div>
        <p class="font-display text-sm text-champagne/90">
          Kepada Yth. Bapak / Ibu / Saudara(i)
        </p>
        <p class="mt-2 font-display text-xl text-champagne sm:text-2xl">
          {{ guestName }}
        </p>
        <div class="mx-auto mt-4 h-px w-48 bg-champagne/35" />
          <p class="mx-auto mt-3 max-w-xs text-[11px] leading-relaxed text-champagne/70">
            Mohon maaf bila penulisan nama, gelar dan alamat tidak sesuai
          </p>
          <div class="mx-auto mt-3 h-px w-48 bg-champagne/35" />
      </div>
      <button
          type="button"
          class="inline-flex min-h-12 min-w-[220px] cursor-pointer items-center justify-center rounded-full border border-champagne/50 bg-burgundy px-8 py-3 font-display text-sm tracking-[0.2em] text-champagne uppercase transition duration-200 hover:bg-burgundy-soft focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-4 focus-visible:outline-champagne active:scale-[0.98]"
          @click="$emit('open')"
        >
          Buka Undangan
        </button>
    </div>
    </div>
  </section>>
</template>