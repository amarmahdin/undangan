<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'

const props = defineProps({
    delay: { type: Number, default: 0 },
})
</script>