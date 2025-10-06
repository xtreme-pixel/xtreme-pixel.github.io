<script setup lang="ts">
import { h } from 'vue'
import type { TableColumn } from '@nuxt/ui'
import { useClipboard } from '@vueuse/core';

useHead({
  title: 'Random Option',
  meta: [
    { name: 'description', content: 'Sistema de random option en Xtreme Pixel' }
  ]
})

const npc_site = ref('/navi prontera 147/174'); // Or get it from an input field
const { copy, copied } = useClipboard();

type EnchantOption = {
  level: string
  min: number
  max: number
  type: string
  category: string
}

const data = ref<EnchantOption[]>([
  { level: 'W Lv1', min: 1, max: 2, type: '+%ATK |+%MATK', category: 'Weapon' },
  { level: 'W Lv1', min: 1, max: 3, type: '+STATS', category: 'Weapon' },
  { level: 'W Lv2', min: 1, max: 5, type: '+%ATK | +%MATK', category: 'Weapon' },
  { level: 'W Lv2', min: 1, max: 5, type: '+STATS', category: 'Weapon' },
  { level: 'W Lv3', min: 5, max: 10, type: '+%ATK | +%MATK', category: 'Weapon' },
  { level: 'W Lv3', min: 3, max: 7, type: '+STATS', category: 'Weapon' },
  { level: 'W Lv4', min: 7, max: 15, type: '+%ATK | +%MATK', category: 'Weapon' },
  { level: 'W Lv4', min: 5, max: 10, type: '+STATS', category: 'Weapon' },
  { level: 'Helm Mid Lower', min: 3, max: 10, type: '-% Reduces After-Cast Delay', category: 'Armor' },
  { level: 'Helm Mid Lower', min: 1, max: 10, type: '+STATS', category: 'Armor' },
  { level: 'Armor', min: 5, max: 15, type: '%HP', category: 'Armor' },
  { level: 'Armor', min: 1, max: 10, type: '+STATS', category: 'Armor' },
  { level: 'Shield', min: 2, max: 5, type: '%ResistRace', category: 'Armor' },
  { level: 'Shield', min: 1, max: 10, type: '+STATS', category: 'Armor' },
  { level: 'Robe', min: 2, max: 5, type: '%SP', category: 'Armor' },
  { level: 'Robe', min: 1, max: 10, type: '+STATS', category: 'Armor' },
  { level: 'Shoes', min: 3, max: 10, type: 'Speed Move%', category: 'Armor' },
  { level: 'Shoes', min: 1, max: 10, type: '+STATS', category: 'Armor' },
  { level: 'Accessory', min: 1, max: 5, type: '+%ATK | +%MATK', category: 'Accessory' },
  { level: 'Accessory', min: 1, max: 10, type: '+STATS', category: 'Accessory' },
  // Nuevos items de Costume
  { level: 'Costume Helm Mid Lower', min: 3, max: 10, type: '+STR, INT, DEX', category: 'Costume' },
  { level: 'Costume Helm Mid Lower', min: 3, max: 10, type: '+AGI, VIT, LUK', category: 'Costume' },
  { level: 'Costume Garment', min: 3, max: 10, type: '+STR, INT, DEX', category: 'Costume' },
  { level: 'Costume Garment', min: 3, max: 10, type: '+AGI, VIT, LUK', category: 'Costume' }
])

// Estadísticas de encantamientos
const enchantStats = ref({
  totalOptions: data.value.length,
  weaponOptions: data.value.filter(item => item.category === 'Weapon').length,
  armorOptions: data.value.filter(item => item.category === 'Armor').length,
  costumeOptions: data.value.filter(item => item.category === 'Costume').length,
  accessoryOptions: data.value.filter(item => item.category === 'Accessory').length
})

const columns: TableColumn<EnchantOption>[] = [
  {
    accessorKey: 'level',
    header: 'Tipo',
    cell: ({ row }) => h('div', { 
      class: 'font-bold text-gray-900 dark:text-white text-sm' 
    }, row.getValue('level'))
  },
  {
    accessorKey: 'min',
    header: 'Min',
    cell: ({ row }) => h('div', { 
      class: 'text-center font-semibold text-blue-600 dark:text-blue-400' 
    }, row.getValue('min'))
  },
  {
    accessorKey: 'max',
    header: 'Max',
    cell: ({ row }) => h('div', { 
      class: 'text-center font-semibold text-green-600 dark:text-green-400' 
    }, row.getValue('max'))
  },
  {
    accessorKey: 'type',
    header: 'Enchant',
    cell: ({ row }) => {
      const type = row.getValue('type') as string
      const isStats = type === '+STATS'
      const isAttack = type.includes('%ATK') || type.includes('%MATK')
      
      let colorClass = 'text-gray-700 dark:text-gray-300'
      if (isStats) colorClass = 'text-blue-600 dark:text-blue-400 font-bold'
      if (isAttack) colorClass = 'text-red-600 dark:text-red-400 font-bold'
      
      return h('div', { 
        class: `font-medium ${colorClass} text-sm leading-tight` 
      }, type)
    }
  },
  {
    accessorKey: 'category',
    header: 'Categoria',
    cell: ({ row }) => {
      const category = row.getValue('category') as string
      const colorClass = {
        'Weapon': 'bg-red-100 text-red-800 dark:bg-red-900 dark:text-red-300',
        'Armor': 'bg-blue-100 text-blue-800 dark:bg-blue-900 dark:text-blue-300',
        'Accessory': 'bg-purple-100 text-purple-800 dark:bg-purple-900 dark:text-purple-300',
        'Costume': 'bg-pink-100 text-pink-800 dark:bg-pink-900 dark:text-pink-300'
      }[category] || 'bg-gray-100 text-gray-800 dark:bg-gray-900 dark:text-gray-300'

      return h('span', { 
        class: `inline-flex items-center px-2.5 py-1 rounded-full text-xs font-bold ${colorClass}`
      }, category)
    }
  }
]

// Filtrar por categoría
const selectedCategory = ref('Todas')
const categories = ['Todas', 'Weapon', 'Armor', 'Accessory', 'Costume']

const filteredData = computed(() => {
  if (selectedCategory.value === 'Todas') {
    return data.value
  }
  return data.value.filter(item => item.category === selectedCategory.value)
})
</script>

<template>
  <div class="min-h-screen bg-gradient-to-br from-blue-50 to-indigo-100 dark:from-gray-900 dark:to-blue-900">
    <!-- Header Hero -->
    <div class="relative bg-gradient-to-r from-purple-600 via-blue-600 to-indigo-700 text-white py-16">
      <div class="absolute inset-0 bg-black/20"></div>
      <UContainer class="relative z-10">
        <div class="text-center">
          <h1 class="text-4xl font-bold mb-4 bg-gradient-to-r from-yellow-300 to-orange-300 bg-clip-text text-transparent">
            Sistema de Encantamiento
          </h1>
          <p class="text-xl mb-6 text-blue-100">
            Random Options para equipamiento normal y costume
          </p>
          <div class="inline-flex items-center gap-4 bg-white/10 backdrop-blur-sm px-6 py-3 rounded-full">
            <UIcon name="i-heroicons-sparkles" class="text-yellow-300" />
            <span class="text-sm">Costo en Zeny • No se rompe al fallar</span>
          </div>
        </div>
      </UContainer>
    </div>

    <UContainer class="py-12">
      <!-- Tarjetas de estadísticas -->
      <div class="grid grid-cols-1 md:grid-cols-4 gap-6 mb-12">
        <UCard class="text-center bg-white/80 dark:bg-gray-800/80 backdrop-blur-sm">
          <template #header>
            <h3 class="text-lg font-semibold text-gray-900 dark:text-white">Total Opciones</h3>
          </template>
          <div class="text-3xl font-bold text-purple-600 dark:text-purple-400">
            {{ enchantStats.totalOptions }}
          </div>
          <p class="text-sm text-gray-600 dark:text-gray-400 mt-2">Encantamientos disponibles</p>
        </UCard>

        <UCard class="text-center bg-white/80 dark:bg-gray-800/80 backdrop-blur-sm">
          <template #header>
            <h3 class="text-lg font-semibold text-gray-900 dark:text-white">Armas</h3>
          </template>
          <div class="text-3xl font-bold text-red-600 dark:text-red-400">
            {{ enchantStats.weaponOptions }}
          </div>
          <p class="text-sm text-gray-600 dark:text-gray-400 mt-2">Niveles 1-4</p>
        </UCard>

        <UCard class="text-center bg-white/80 dark:bg-gray-800/80 backdrop-blur-sm">
          <template #header>
            <h3 class="text-lg font-semibold text-gray-900 dark:text-white">Armaduras</h3>
          </template>
          <div class="text-3xl font-bold text-blue-600 dark:text-blue-400">
            {{ enchantStats.armorOptions }}
          </div>
          <p class="text-sm text-gray-600 dark:text-gray-400 mt-2">Varios tipos</p>
        </UCard>

        <UCard class="text-center bg-white/80 dark:bg-gray-800/80 backdrop-blur-sm">
          <template #header>
            <h3 class="text-lg font-semibold text-gray-900 dark:text-white">Costumes</h3>
          </template>
          <div class="text-3xl font-bold text-pink-600 dark:text-pink-400">
            {{ enchantStats.costumeOptions }}
          </div>
          <p class="text-sm text-gray-600 dark:text-gray-400 mt-2">Nuevos items</p>
        </UCard>
      </div>

      <!-- Filtros por categoría -->
      <UCard class="mb-6">
        <template #header>
          <h3 class="text-lg font-semibold text-gray-900 dark:text-white mb-2">
            Filtrar por Categoría
          </h3>
        </template>
        <div class="flex flex-wrap gap-2">
          <UButton
            v-for="category in categories"
            :key="category"
            :color="selectedCategory === category ? 'primary' : 'gray'"
            variant="solid"
            @click="selectedCategory = category"
            class="mb-2"
            size="sm"
          >
            {{ category }}
            <template v-if="category !== 'Todas'">
              <span class="ml-1 bg-white/20 px-1.5 py-0.5 rounded text-xs">
                {{ data.filter(item => item.category === category).length }}
              </span>
            </template>
          </UButton>
        </div>
      </UCard>

      <!-- Tabla de Encantamientos -->
      <UCard class="mb-12">
        <template #header>
          <div class="flex items-center justify-between">
            <div>
              <h2 class="text-2xl font-bold text-gray-900 dark:text-white flex items-center gap-2">
                <UIcon name="i-heroicons-sparkles" class="text-purple-500" />
                Enchant Random Options
              </h2>
              <p class="text-gray-600 dark:text-gray-400 mt-1">
                Lista completa de Random Option con sus valores mínimos/máximos y equipamiento.
                El costo de este trabajo es en Zeny y al fallar no rompe el equipamiento.
              </p>
            </div>
            <UBadge color="purple" variant="solid" size="lg">
              {{ filteredData.length }} Items
            </UBadge>
          </div>
        </template>

        <div class="overflow-x-auto">
          <UTable 
            :data="filteredData" 
            :columns="columns" 
            class="flex-1 min-w-max"
            :ui="{
              wrapper: 'ring-1 ring-gray-200 dark:ring-gray-800 rounded-lg overflow-hidden',
              thead: 'bg-gradient-to-r from-purple-50 to-indigo-50 dark:from-purple-900/20 dark:to-indigo-900/20',
              tbody: 'divide-y divide-gray-200 dark:divide-gray-800',
              th: 'py-4 px-4 text-left font-bold text-gray-900 dark:text-white',
              td: 'py-3 px-4'
            }"
          />
        </div>

        <!-- Información adicional -->
        <div class="mt-6 grid grid-cols-1 md:grid-cols-2 gap-4 text-sm">
          <div class="p-4 bg-blue-50 dark:bg-blue-900/20 rounded-lg">
            <h4 class="font-semibold text-blue-800 dark:text-blue-300 mb-2 flex items-center gap-2">
              <UIcon name="heroicons-information-circle" class="text-blue-500" />
              Información Importante
            </h4>
            <ul class="text-blue-700 dark:text-blue-400 space-y-1">
              <li>• Sistema seguro: No se pierde el equipo al fallar</li>
              <li>• Costo en Zeny: No requiere items especiales</li>
              <li>• Encantamiento multiple: Cada vez que encantas, incrusta dos encantamientos</li>
            </ul>
          </div>
          <div class="p-4 bg-green-50 dark:bg-green-900/20 rounded-lg">
            <h4 class="font-semibold text-green-800 dark:text-green-300 mb-2 flex items-center gap-2">
              <UIcon name="heroicons-light-bulb" class="text-green-500" />
              Tips de Encantamiento
            </h4>
            <ul class="text-green-700 dark:text-green-400 space-y-1">
              <li>• Los stats son totalmente aleatorios</li>
              <li>• +%ATK/MATK ideal para personajes de daño</li>
              <li>• Los costumes ahora pueden recibir encantamientos</li>
            </ul>
          </div>
        </div>
      </UCard>

      <!-- Sección de Costumes -->
      <UCard class="mb-12">
        <template #header>
          <div class="flex items-center justify-between">
            <div>
              <h2 class="text-2xl font-bold text-gray-900 dark:text-white flex items-center gap-2">
                <UIcon name="i-heroicons-star" class="text-pink-500" />
                Nuevo: Encantamientos para Costumes
              </h2>
              <p class="text-gray-600 dark:text-gray-400 mt-1">
                Ahora puedes aplicar encantamientos +STATS a tus items de costume favoritos
              </p>
            </div>
            <UBadge color="pink" variant="solid">
              Nuevo
            </UBadge>
          </div>
        </template>

        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
          <div class="text-center p-6 bg-gradient-to-br from-pink-50 to-rose-50 dark:from-pink-900/20 dark:to-rose-900/20 rounded-xl">
            <UIcon name="game-icons-pointy-hat" class="text-4xl text-pink-500 mb-4" />
            <h3 class="text-lg font-bold text-gray-900 dark:text-white mb-2">Costume Hat</h3>
            <p class="text-gray-600 dark:text-gray-400 mb-3">+STATS: 3 - 10</p>
            <UBadge color="pink" variant="subtle">
              Mejora tu apariencia y stats
            </UBadge>
          </div>
          <div class="text-center p-6 bg-gradient-to-br from-purple-50 to-indigo-50 dark:from-purple-900/20 dark:to-indigo-900/20 rounded-xl">
            <UIcon name="i-heroicons-clipboard-document" class="text-4xl text-purple-500 mb-4" />
            <h3 class="text-lg font-bold text-gray-900 dark:text-white mb-2">Costume Garment</h3>
            <p class="text-gray-600 dark:text-gray-400 mb-3">+STATS: 3 - 10</p>
            <UBadge color="purple" variant="subtle">
              Capas con beneficios
            </UBadge>
          </div>
        </div>
      </UCard>

      <!-- Call to Action -->
      <div class="text-center p-8 bg-gradient-to-r from-purple-500 to-indigo-600 rounded-2xl text-white shadow-xl">
        <h2 class="text-3xl font-bold mb-4">¿Listo para Mejorar tu Equipo?</h2>
        <p class="text-xl mb-6 text-purple-100">
          Visita al NPC Random Option Master para comenzar a encantar tu equipo
        </p>
        <div class="flex flex-col sm:flex-row gap-4 justify-center">
          <UButton 
            size="xl" 
            :color="copied ? 'warning' : 'white'"
            variant="solid"
            class="font-bold text-purple-600 hover:scale-105 transition-transform"
            @click="copy(npc_site)"
          >
            <UIcon name="i-heroicons-map-pin" class="w-5 h-5" />
            Click para copiar la ubicación y pegar en el chat del juego
          </UButton>
        </div>
      </div>
    </UContainer>
  </div>
</template>