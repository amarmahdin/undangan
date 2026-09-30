<script setup>
import Ornament from './Ornament.vue'

defineProps({
  dateLabel: { type: String, default: '' },
  city: { type: String, default: '' },
  showScroll: { type: Boolean, default: false },
})
</script>