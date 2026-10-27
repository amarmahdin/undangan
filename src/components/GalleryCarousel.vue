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
  
})
</script>