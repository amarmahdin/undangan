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
</script>