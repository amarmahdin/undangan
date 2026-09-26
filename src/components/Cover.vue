<script setup>
import Ornament from './Ornament.vue'

defineProps({
  guestName: { type: String, required: true },
  visible: { type: Boolean, default: true },
})

defineEmits(['open'])

const floralStyle = {
 
}
</script>