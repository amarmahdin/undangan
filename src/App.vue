<script setup>
import { computed, onMounted, ref } from 'vue'
import Cover from './components/Cover.vue'
import InvitationPage from './components/InvitationPage.vue'
import { invitation } from './data/invitation.js'

const opened = ref(false)
const guestName = ref('')

const greetingName = computed(() => guestName.value.trim() || 'Bapak / Ibu / Saudara(i)')

function openInvitation() {
  opened.value = true
  document.body.style.overflow = ''
}

onMounted(() => {
  const params = new URLSearchParams(window.location.search)
  guestName.value = params.get('to') || params.get('nama') || ''
  document.body.style.overflow = 'hidden'
})
</script>

<template>
  <a
    href="#undangan"
    class="sr-only focus:not-sr-only focus:absolute focus:left-4 focus:top-4 focus:z-[80] focus:rounded-md focus:bg-champagne focus:px-4 focus:py-2 focus:text-burgundy"
  >
    Lewati ke isi undangan
  </a>

  <Cover
    :guest-name="greetingName"
    :visible="!opened"
    @open="openInvitation"
  />

  <InvitationPage
    id="undangan"
    :invitation="invitation"
    :opened="opened"
  />
</template>
