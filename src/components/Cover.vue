<script setup>
import Ornament from './Ornament.vue'

defineProps({
  guestName: { type: String, required: true },
  visible: { type: Boolean, default: true },
})

defineEmits(['open'])

const floralStyle = {
  backgroundImage: `url(${import.meta.env.BASE_URL}images/floral-line.jpg)`,
  backgroundSize: 'cover',
  backgroundPosition: 'center',
}
</script>