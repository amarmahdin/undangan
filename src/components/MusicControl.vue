<script setup>
import { onBeforeUnmount, ref, watch } from 'vue'

const props = defineProps({
  src: { type: String, required: true },
  active: { type: Boolean, default: false },
  volume: { type: Number, default: 0.45 },
})

const playing = ref(false)
const ready = ref(false)
const audio = ref(null)

function ensureAudio() {
    if (audio.value) return audio.value
    const el = new Audio(props.src)
    el.loop = true
    el.preload = 'auto'
    el.volume = Math.min(1, Math.max(0, props.volume))
    el.addEventListener('canplaythrough', () => {
        ready.value = true
    })
    el.addEventListener('play', () => {
        playing.value = true
    })
    audio.value = el
    return el
}

async function play() {
    
}
</script>