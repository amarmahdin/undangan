<script setup>
import { onBeforeUnmount, ref, watch } from 'vue'

const props = defineProps({
  src: { type: String, required: true },
  active: { type: Boolean, default: false },
  volume: { type: Number, default: 0.45 },
})
</script>