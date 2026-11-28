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
    const el = ensureAudio()
    try {
        await el.play()
        playing.value = true
    } catch {
        playing.value = false
    }
}

function pause() {
    audio.value?.pause()
    playing.value = false
}

async function toggle() {
    if (playing.value) pause()
    else await play()
}

watch(
    () => props.active,
    async (value) => {
        if (value) await play()
        else pause()
    },
)

onBeforeUnmount(() => {
    pause()
    if (audio.value) {
        audio.value.src = ''
        audio.value = null
    }
})

defineExpose({ play, pause, toggle })
</script>

<template>
    <button
        v-show="active"
        type="button"
        class="music-btn fixed bottom-[max(1.25rem,env(safe-area-inset-bottom))] right-4 z-[60] flex h-12 w-12 cursor-pointer items-center justify-center rounded-full border border-gold/45 bg-burgundy text-champagne shadow-[0_12px_28px_rgba(48,16,24,0.35)] transition duration-200 hover:bg-burgundy-soft focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-4 focus-visible:outline-gold active:scale-95 sm:right-6"
        class="music-btn fixed bottom-[max(1.25rem,env(safe-area-inset-bottom))] right-4 z-[60] flex h-12 w-12 cursor-pointer items-center justify-center rounded-full border border-gold/45 bg-burgundy text-champagne shadow-[0_12px_28px_rgba(48,16,24,0.35)] transition duration-200 hover:bg-burgundy-soft focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-4 focus-visible:outline-gold active:scale-95 sm:right-6"
        :aria-label="playing ? 'Matikan musik' : 'Hidupkan musik'"
        :aria-pressed="playing"

    >

    </button>
</template>