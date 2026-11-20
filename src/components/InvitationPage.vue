<script setup>
import { computed, onBeforeUnmount, onMounted, reactive, watch } from 'vue'
import GalleryCarousel from './GalleryCarousel.vue'
import EventOval from './EventOval.vue'
import FloralCorner from './FloralCorner.vue'
import GiftSection from './GiftSection.vue'
import HeroStage from './HeroStage.vue'
import LoveStory from './LoveStory.vue'
import Reveal from './Reveal.vue'
import WishForm from './WishForm.vue'

const props = defineProps({
  invitation: { type: Object, required: true },
  opened: { type: Boolean, default: false },
})

const remaining = reactive  ({
  days: 0,
  hours: 0,
  minutes: 0,
  seconds: 0,
  done: false,
})

const heroReady = refShow()

function refShow() {
  return reactive({ show: false })
}

let timer

function pad(value) {
  return String(value).padStart(2, '0')
}

function updateCountdown () {
  const target = new Date(props.invitation.targetDate).getTime()
  const diff = target - Date.now()
  if (diff <= 0) {
    remaining.done = true
    remaining.days = remaining.hours = remaining.minutes = remaining.seconds = 0
    return
  }
  remaining.done = false
  remaining.days = Math.floor(diff / 86400000)
  remaining.hours = Math.floor((diff % 86400000) / 3600000)
  remaining.minutes = Math.floor((diff % 3600000) / 60000)
  remaining.seconds = Math.floor((diff % 60000) / 1000)
}

const mapsLink = computed(() => {
  const q = encodeURIComponent(props.invitation.venue.mapsQuery)
  return `https://www.google.com/maps/search/?api=1&query=${q}`
})

const asset = (file) => `${import.meta.env.BASE_URL}images/${file}`

watch(
  () => props.opened,
  (value) => {
    if (value) {
      heroReady.show = false
      window.setTimeout(() => {
        heroReady.show = true
      }, 320)
    }
  },
  { immediate: true },
)

onMounted(() => {
  updateCountdown()
  timer = window.setInterval(updateCountdown, 1000)
})

onBeforeUnmount(() => {
  window.clearInterval(timer)
})
</script>

<template>
  <div 
  class="silk-bg max-w-[100vw] overflow-x-clip text-ink transition-opacity duration-700"
  :class="opened ? 'opacity-100' : 'pointer-events-none max-h-dvh overflow-hidden opacity-0'"
  >
    <section
    class="relative overflow-hidden"
    :class="heroReady.show ? 'hero-enter-in' : 'hero-enter'"
    >
      <HeroStage
      :date-label="invitation.dateLabel"
      :city="invitation.city"
      show-scroll
      />
    </section class="section-luxury mx-auto max-w-3xl px-5 py-16 text-center sm:py-20">
      <Reveal from="up" class="relative z-[1]">
        <Ornament class="mx-auto mb-6 w-28 text-gold/70" />
        <p class="font-display text-lg italic leading-relaxed text-burgundy sm:text-xl">
          “{{ invitation.quote }}”
        </p>
        <p class="mt-5 font-display tracking-[0.16em] text-gold-deep uppercase">
          ( {{ invitation.quoteSource }} )
        </p>
      </Reveal>
    <section class="relative mx-auto max-w-5xl px-5 pb-16 sm:pb-24">
      <div class="pointer-events-none absolute -left-2 -top-6 z-[2] w-36 opacity-90 sm:-left-8 sm:-top-8 sm:w-48">
        <FloralCorner side="left" />
      </div>
      <div class="pointer-events-none absolute -bottom-4 -right-2 z-[2] w-32 opacity-90 sm:-bottom-6 sm:-right-6 sm:w-44">
        <FloralCorner side="right" />
      </div>
    </section>
  </div>

  <div class="invite-panel relative z-[1] px-5 py-10 sm:px-12 sm:py-12">
    <Reveal from="fade">
      <p class="text-center font-display text-lg text-burgundy sm:text-xl">
        {{ invitation.greeting }}
      </p>
      <p class="mx-auto mt-5 max-w-2xl text-center text-base leading-relaxed text-muted">
        {{ invitation.intro }}
      </p>
    </Reveal>

    <div class="mt-12 grid gap-12 md:grid-cols-[1fr_auto_1fr] md:items-start md:gap-8">
      <Reveal from="soft" :delay="80">
        <article class="flex flex-col items-center text-center">
          <div class="photo-frame photo-frame-anim w-[58%] max-w-[200px] sm:w-[70%]">
            <img
              :src="asset(invitation.bride.photo)"
              :alt="invitation.bride.fullName"
              width="800"
              height="1200"
              loading="lazy"
            />
          </div>
          <p class="mt-5 font-display text-[11px] tracking-[0.28em] text-gold-deep uppercase">
            Mempelai Wanita
          </p>
          <p class="mt-2 font-script text-[clamp(1.85rem,5vw,2.75rem)] leading-tight text-gold-deep">
            {{ invitation.bride.fullName }}
          </p>
          <p class="mt-3 max-w-xs text-sm leading-relaxed text-muted">
            {{ invitation.bride.parents }}
          </p>
        </article>
      </Reveal>

      <Reveal
        from="fade"
        :delay="180"
        class="flex items-center justify-center self-center py-2 md:py-16"
      >
        <div class="flex flex-col items-center gap-3">
          <div class="hidden h-12 w-px bg-gold/40 md:block"/>
            <p class="font-display text-xs tracking-[0.4em] text-burgundy uppercase">
                Dengan
            </p>
          <div class="hidden h-12 w-px bg-gold/40 md:block" />
        </div>
      </Reveal>

      <Reveal from="soft" :delay="260">
        <article class="flex flex-col items-center text-center">
          <div class="photo-frame photo-frame-anim w-[58%] max-w-[200px] sm:w-[70%]">
            <img
              :src="asset(invitation.groom.photo)"
              :alt="invitation.groom.fullName"
              width="800"
              height="1200"
            />
          </div>
        </article>
      </Reveal>
    </div>
  </div>
</template>