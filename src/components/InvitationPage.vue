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
</script>