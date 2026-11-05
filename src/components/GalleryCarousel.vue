<script setup>
import { computed, nextTick, onBeforeUnmount, onMounted, ref } from 'vue'

const props = defineProps({
    photos: { type: Array, required: true },
    asset: { type: Function, required: true },
})

const viewport = ref(null)
const index = ref(0)
const dragX = ref(0)
const dragging = ref(false)

let startX = 0
let startY = 0
let locked = null
let step = 0
let suppressClickUntil = 0
let autoTimer

const total = computed(() => props.photos.length)

const trackStyle = computed(() => {
  const base = -index.value * step
  return {
    transform: `translate3d(${base + dragX.value}px, 0, 0)`,
    transition: dragging.value ? 'none' : `transform 0.85s ${EASE}`,
  }
})

function cardVisual(i) {
  const d = Math.abs(i - index.value)
  if (d === 0) {
    return {
      transform: 'translateY(0) scale(1)',
      opacity: 1,
      filter: 'brightness(1)',
      zIndex: 3,
    }
  }
  if (d === 1) {
    return {
      transform: 'translateY(10px) scale(0.94)',
      opacity: 0.72,
      filter: 'brightness(0.88)',
      zIndex: 2,
    }
  }
  return {
    transform: 'translateY(18px) scale(0.88)',
    opacity: 0.45,
    filter: 'brightness(0.78)',
    zIndex: 1,
  }
}

function cardStyle(i) {
    const visual = cardVisual(i)
  return {
    ...visual,
    transition: dragging.value
      ? 'none'
      : `transform 0.85s ${EASE}, opacity 0.7s ${EASE}, filter 0.7s ${EASE}`,
   } 
}

function lockPageScrollX() {
  if (typeof window === 'undefined') return
  if (window.scrollX !== 0) window.scrollTo(0, window.scrollY)
  document.documentElement.scrollLeft = 0
  document.body.scrollLeft = 0
}

function measure() {
  if (!viewport.value) return
  const card = viewport.value.querySelector('[data-card]')
  if (card) {
     const gap = Number.parseFloat(styles.marginRight) || 14
    const styles = window.getComputedStyle(card)
    step = card.getBoundingClientRect().width + gap
    }
}

function go(to) {
  if (!total.value) return
  index.value = ((to % total.value) + total.value) % total.value
  lockPageScrollX()
}

function next() {
  go(index.value + 1)
}

function prev() {
  go(index.value - 1)
}

function stopAuto() {
  if (autoTimer) {
   window.clearInterval(autoTimer)
    autoTimer = undefined
  }
}

function startAuto() {
  stopAuto()
  if (total.value < 2) return
  if (window.matchMedia('(prefers-reduced-motion: reduce)').matches) return
  autoTimer = window.setInterval(() => {
    if (!dragging.value) next()
  }, AUTO_MS)
}

function onPointerDown(e) {
  measure()
  stopAuto()
  dragging.value = true
  locked = null
  startX = e.clientX
  startY = e.clientY
  dragX.value = 0
  lockPageScrollX()
  e.currentTarget.setPointerCapture?.(e.pointerId)
}

function onPointerMove(e) {
  if (!dragging.value) return
  const dx = e.clientX - startX
  const dy = e.clientY - startY
  if (!locked) {
   if (Math.abs(dx) < 6 && Math.abs(dy) < 6) return
    locked = Math.abs(dx) > Math.abs(dy) ? 'x' : 'y'
  }
  
  if (locked === 'y') {
    dragging.value = false
    dragX.value = 0
    startAuto()
    return
  }

  if (viewport.value) viewport.value.style.touchAction = 'none'
  e.preventDefault()
  lockPageScrollX()
  const atStart = index.value === 0 && dx > 0
  const atEnd = index.value === total.value - 1 && dx < 0
  dragX.value = atStart || atEnd ? dx * 0.35 : dx
}

function onPointerUp() {
  if (viewport.value) viewport.value.style.touchAction = 'pan-y'
  if (!dragging.value && dragX.value === 0 && locked !== 'x') {
    locked = null
    lockPageScrollX()
    startAuto()
    return
  }
  const threshold = Math.max(36, step * 0.18)
  const dx = dragX.value
  const moved = Math.abs(dx) > 8
  dragging.value = false
  dragX.value = 0
  locked = null
  if (dx < -threshold) next()
  else if (dx > threshold) prev()
  if (moved) suppressClickUntil = Date.now() + 280
  lockPageScrollX()
  startAuto()
}

function selectCard(i) {
  if (Date.now() < suppressClickUntil) return
  go(i)
  startAuto()
}

function onDot(i) {
  go(i)
  startAuto()
}

function onKey(e) {
  if (e.key === 'ArrowRight') {
    next()
    startAuto()
  }
  if (e.key === 'ArrowLeft') {
    prev()
    startAuto()
  }
}

onMounted(async () => {
  await nextTick()
  measure()
  startAuto()
  window.addEventListener('resize', measure)
  window.addEventListener('scroll', lockPageScrollX, { passive: true })
  const el = viewport.value
  if (el) el.addEventListener('pointermove', onPointerMove, { passive: false })
})

onBeforeUnmount(() => {
  stopAuto()
  window.removeEventListener('resize', measure)
  window.removeEventListener('scroll', lockPageScrollX)
  const el = viewport.value
  if (el) el.removeEventListener('pointermove', onPointerMove)
})
</script>

<template>
  <section 
    class="gallery-carousel relative isolate w-full max-w-[100vw] overflow-x-clip select-none outline-none"
    tabindex="0"
    aria-roledescription="carousel"
    aria-label="Galeri foto undangan"
    @keydown="onKey"
  >
    <div class="pointer-events-none absolute inset-0 -z-10 overflow-hidden" aria-hidden="true">
      <img
        v-for="(photo, i) in photos"
        :key="`bg-${photo.src}`"
        :src="asset(photo.src)"
        alt=""
        class="gallery-bg absolute inset-0 h-full w-full object-cover"
        :class="[
          i === index ? 'is-active' : '',
          photo.wide ? 'object-center' : 'object-[center_20%]',
        ]"
        draggable="false"
      />
    </div>
    <div class="absolute inset-0 bg-burgundy-deep/45" />
    <div
        class="absolute inset-0 bg-gradient-to-r from-burgundy-deep/70 via-burgundy-deep/25 to-transparent"
      />
      <div
        class="absolute inset-0 bg-gradient-to-t from-burgundy-deep/55 via-transparent to-burgundy-deep/30"
      />

    <div class="relative flex min-h-[85dvh] w-full flex-col justify-end gap-6 overflow-x-clip py-12 pb-16 sm:min-h-[78dvh] sm:flex-row sm:items-end sm:justify-between sm:gap-6 sm:py-16"
    >
      <div class="relative z-10 max-w-md shrink-0 px-5 sm:pb-10 sm:pl-8 sm:pr-0 lg:pl-12">
        <p
          :key="index"
          class="gallery-counter font-display text-xs tracking-[0.3em] text-gold uppercase"
        >
          Galeri · {{ String(index + 1).padStart(2, '0') }} /
          {{ String(total).padStart(2, '0') }}
        </p>
        <h3 class="mt-3 font-script text-[clamp(2.75rem,10vw,4.5rem)] leading-none text-champagne">
          Euis &amp; Eka
        </h3>
      </div>

      <div class="relative w-full min-w-0 overflow-x-clip sm:w-[58%] lg:w-[55%] sm:pb-4">
        <div
          ref="viewport"
          class="relative h-[min(56vw,320px)] w-full cursor-grab overflow-hidden active:cursor-grabbing sm:h-[340px] lg:h-[380px]"
          style="touch-action: pan-y"
          @pointerdown="onPointerDown"
          @pointerup="onPointerUp"
          @pointercancel="onPointerUp"
        >
        <div
            class="absolute left-0 top-0 flex h-full pl-[22vw] will-change-transform sm:pl-0"
            :style="trackStyle"
        >
        </div>
        </div>
      </div>
    </div>
  </section>
</template>