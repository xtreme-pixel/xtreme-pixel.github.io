<script setup lang="ts">
    import type { NavigationMenuItem } from '@nuxt/ui';

    const route = useRoute();

    const items = computed<NavigationMenuItem[]>(() => [{
        label: 'Server-Info',
        to: '/',
        icon: 'i-lucide-book-open',
        }, {
        label: 'Random Options',
        to: '/random_option',
        icon: 'game-icons-perspective-dice-six-faces-random',
        }, {
        label: 'Refine',
        icon: 'icon-park-outline-hammer-and-anvil',
        to: '/refine',
        target: ''
        }, {
        label: 'Skill Mejoradas',
        icon: 'game-icons-boss-key',
        to: '/skills',
        target: '',
        }, 
        {
        label: 'Comandos',
        icon: 'mdi-at',
        to: '/commands',
        target: '',
        }, {
        label: 'Download',
        icon: 'i-lucide-download',
        to: '/download',
        target: '',
        },
    ]);
</script>

<template>
  <UHeader toggle-side="left">
    <template #title>
        
        <!-- <Logo class="h-6 w-auto" /> aqui ira mi logo -->

        <img
          src="/favicon.ico"
          class="h-8 w-auto"
        />

        Xtreme-Pixel

    </template>

    <UNavigationMenu :items="items" />

    <template #right>
      <UColorModeButton />

        <UButton
          color="neutral"
          variant="ghost"
          to="https://discord.gg/66f3ZfPKBY"
          target="_blank"
          icon="i-simple-icons-discord"
          aria-label="GitHub"
        />
    </template>

    <template #body>
      <UNavigationMenu :items="items" orientation="vertical" class="-mx-2.5" />
    </template>
  </UHeader>
</template>

