<template>
    <div>
        <NavBar />
        <NuxtPage />
    </div>
</template>

<script setup lang="ts">
// app.vue - Configuración global
useHead({
  titleTemplate: '%s ❤️ XtremePixel ❤️',
  meta: [
    { charset: 'utf-8' },
    { name: 'viewport', content: 'width=device-width, initial-scale=1' }
  ]
})
</script>