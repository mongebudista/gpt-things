<script setup lang="ts">
const links = [{
  label: 'Chat',
  icon: 'i-heroicons-book-open-solid',
  to: '/chat'
}, {
  label: 'Image',
  icon: 'i-simple-icons-stackblitz',
  to: '/image'
}]
</script>

<template>
  <UAsideLinks :links="links" />
</template>