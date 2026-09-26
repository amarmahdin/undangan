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
    ([entry]) => {
        if (entry.isIntersecting) {
        shown.value = true
        observer?.disconnect()
      }
    },
    { threshold: 0.12, rootMargin: '0px 0px -6% 0px' },
  )
  if (root.value) observer.observe(root.value)
})

onBeforeUnmount(() => observer?.disconnect())
</script>