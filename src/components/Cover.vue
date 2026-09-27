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

<template>  
  <section
    :class="fixed inset-0 z-50 flex items-center justify-center overflow-hidden bg-burgundy-deep transition-[transform,opacity] duration-700 ease-[cubic-bezier(0.22,1,0.36,1)]"
    class="fixed inset-0 z-50 flex items-center justify-center overflow-hidden bg-burgundy-deep transition-[transform,opacity] duration-700 ease-[cubic-bezier(0.22,1,0.36,1)]"
    
  > 

  </section>>
</template>