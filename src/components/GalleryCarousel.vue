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

}
</script>