<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'

const props = defineProps({
    delay: { type: Number, default: 0 },
    from: { type: String, default: 'up' }, // up | left | right | fade | scale
})

const root = ref(null)
const shown = ref(false)
let observer

onMounted(() => {
  observer = new IntersectionObserver(
    
  )
})

</script>