<script setup lang="ts">
import { h } from 'vue'
import type { TableColumn } from '@nuxt/ui'

useHead({
  title: 'Info',
  meta: [
    { name: 'description', content: 'Información basica del servidor' }
  ]
})

// Datos de Rates
const ratesData = ref([
  { category: 'Base Exp', value: '8500x' },
  { category: 'Job Exp', value: '8500x' },
  { category: 'Quest Exp', value: '10x' },
  { category: 'Mvp Exp', value: '1000x' },
  { category: 'Normal Drop Rate', value: '500x' },
  { category: 'Normal Card', value: '5.0%' },
  { category: 'Boss Card', value: '5.0%' },
  { category: 'MvP Card', value: '5.0%' }
])

// Datos de NPCs
const npcsData = ref([
  { npc: 'Healer', description: 'Blessing & Increase Agility' },
  { npc: 'Warper', description: 'Cities, Dungeons, Fields, Branch Rooms y Special Zones' },
  { npc: 'Battle Recruiter', description: 'PVP, BG, Arena, 1 vs 1, Deathmatch y GVG' },
  { npc: 'Job Master', description: 'Cambio de job' },
  { npc: 'Build Manager', description: 'Shortcut Storage, Status Storage, Skill/Stats Reset, Platinum Skill, Homunculus Reset, Feel Reset, Hatred Reset, TK Mission Reset' },
  { npc: 'Tool Dealer', description: 'Sell, Consumables, Arrows/Ammo, Equipment, Weapons, Forging Shop, Alchemist Shop, Pet Shop' },
  { npc: 'Random Option Master', description: 'Enchant Equipment' }
])

// Información del servidor
const serverInfo = ref({
  episode: '14+ ~ Bifrost',
  maxBaseLevel: 255,
  maxJobLevel: 100,
  type: 'Old School - PreRenewal',
  customItems: 'No'
})

// Columnas para Rates
const ratesColumns: TableColumn<any>[] = [
  {
    accessorKey: 'category',
    header: 'Categoría',
    cell: ({ row }) => h('div', { 
      class: 'font-bold text-gray-900 dark:text-white' 
    }, row.getValue('category'))
  },
  {
    accessorKey: 'value',
    header: 'Valor',
    cell: ({ row }) => {
      const value = row.getValue('value') as string
      const isPercentage = value.includes('%')
      const isExp = value.includes('x') && !isPercentage
      
      let colorClass = 'text-gray-700 dark:text-gray-300'
      if (isPercentage) colorClass = 'text-red-600 dark:text-red-400 font-bold text-lg'
      if (isExp) colorClass = 'text-green-600 dark:text-green-400 font-bold text-lg'
      
      return h('div', { class: `${colorClass} text-center` }, row.getValue('value'))
    }
  }
]

// Columnas para NPCs
const npcsColumns: TableColumn<any>[] = [
  {
    accessorKey: 'npc',
    header: 'NPC',
    cell: ({ row }) => {
      const npc = row.getValue('npc') as string
      return h('div', { 
        class: 'bg-blue-100 dark:bg-blue-900 text-blue-800 dark:text-blue-300 px-4 py-2 rounded-full font-medium text-center' 
      }, npc)
    }
  },
  {
    accessorKey: 'description',
    header: 'Descripción',
    cell: ({ row }) => {
      const description = row.getValue('description') as string
      return h('div', { 
        class: 'text-gray-700 dark:text-gray-300 leading-tight' 
      }, description || 'Funcionalidades básicas')
    }
  }
]


const open = ref(true)

defineShortcuts({
  o: () => open.value = !open.value
})
</script>

<template>

  <UModal v-model:open="open" title="Falta poco para la apertura" :close="false" size="md" description="Estamos afinando detalles para brindarte la mejor experiencia. ¡Pronto estaremos en línea!">
    <template #footer>
      <div class="w-full text-right">
        <UButton color="warning" variant="solid" @click="open = false" href="https://discord.gg/66f3ZfPKBY" target="_blank">Cerrar</UButton>
      </div>
    </template>
  </UModal>


  <div class="min-h-screen bg-gradient-to-br from-blue-50 to-indigo-100 dark:from-gray-900 dark:to-blue-900">
    <!-- Header Hero -->
    <div class="relative bg-gradient-to-r from-purple-600 via-blue-600 to-indigo-700 text-white py-20">
      <div class="absolute inset-0 bg-black/20"></div>
      <UContainer class="relative z-10">
        <div class="text-center">
          <h1 class="text-5xl font-bold mb-4 bg-gradient-to-r from-yellow-300 to-orange-300 bg-clip-text text-transparent">
            Xtreme Pixel 255/100
          </h1>
          <p class="text-xl mb-8 text-blue-100">
            Servidor Old School Pre-Renewal • Episode 14 - Bifrost
          </p>
          <div class="flex justify-center gap-4">
            <UButton 
              size="xl" 
              color="white" 
              variant="solid"
              class="font-bold"
              to="/download"
            >
              Descargar Cliente
            </UButton>
            <UButton 
              size="xl" 
              color="gray" 
              variant="outline"
              class="font-bold border-white text-white hover:bg-white hover:text-gray-900"
              href="https://discord.gg/66f3ZfPKBY"
              target="_blank"
            >
              Unirse al Discord
            </UButton>
          </div>
        </div>
      </UContainer>
    </div>

    <UContainer class="py-12">
      <!-- Tarjetas de información del servidor -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-12">
        <UCard class="text-center bg-white/80 dark:bg-gray-800/80 backdrop-blur-sm hover:shadow-lg transition-shadow">
          <template #header>
            <h3 class="text-lg font-semibold text-gray-900 dark:text-white">Episode</h3>
          </template>
          <div class="text-3xl font-bold text-purple-600 dark:text-purple-400">
            {{ serverInfo.episode }}
          </div>
          <p class="text-sm text-gray-600 dark:text-gray-400 mt-2">Contenido Adaptado</p>
        </UCard>

        <UCard class="text-center bg-white/80 dark:bg-gray-800/80 backdrop-blur-sm hover:shadow-lg transition-shadow">
          <template #header>
            <h3 class="text-lg font-semibold text-gray-900 dark:text-white">Niveles Máximos</h3>
          </template>
          <div class="space-y-2">
            <div class="flex justify-between items-center">
              <span class="text-gray-600 dark:text-gray-400">Base:</span>
              <span class="text-2xl font-bold text-green-600 dark:text-green-400">{{ serverInfo.maxBaseLevel }}</span>
            </div>
            <div class="flex justify-between items-center">
              <span class="text-gray-600 dark:text-gray-400">Job:</span>
              <span class="text-2xl font-bold text-blue-600 dark:text-blue-400">{{ serverInfo.maxJobLevel }}</span>
            </div>
          </div>
        </UCard>

        <UCard class="text-center bg-white/80 dark:bg-gray-800/80 backdrop-blur-sm hover:shadow-lg transition-shadow">
          <template #header>
            <h3 class="text-lg font-semibold text-gray-900 dark:text-white">Tipo</h3>
          </template>
          <div class="text-xl font-bold text-orange-600 dark:text-orange-400">
            {{ serverInfo.type }}
          </div>
          <p class="text-sm text-gray-600 dark:text-gray-400 mt-2">No 3 o 4 job</p>
        </UCard>

        <UCard class="text-center bg-white/80 dark:bg-gray-800/80 backdrop-blur-sm hover:shadow-lg transition-shadow">
          <template #header>
            <h3 class="text-lg font-semibold text-gray-900 dark:text-white">Custom Items</h3>
          </template>
          <div class="text-3xl font-bold" :class="serverInfo.customItems === 'No' ? 'text-green-600 dark:text-green-400' : 'text-red-600 dark:text-red-400'">
            {{ serverInfo.customItems }}
          </div>
          <p class="text-sm text-gray-600 dark:text-gray-400 mt-2">Servidor Clásico</p>
        </UCard>
      </div>

      <!-- Grid de dos tablas -->
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 mb-12">
        <!-- Tabla de Rates -->
        <UCard class="h-fit h-auto">
          <template #header>
            <div class="flex items-center justify-between">
              <div>
                <h2 class="text-2xl font-bold text-gray-900 dark:text-white flex items-center gap-2">
                  <UIcon name="i-heroicons-chart-bar" class="text-green-500" />
                  Rates del Servidor
                </h2>
                <p class="text-gray-600 dark:text-gray-400 mt-1">Configuración de experiencias y drops</p>
              </div>
              <UBadge color="green" variant="solid">
                Activos
              </UBadge>
            </div>
          </template>

          <div class="overflow-x-auto">
            <UTable 
              :data="ratesData" 
              :columns="ratesColumns" 
              :ui="{
                wrapper: 'ring-1 ring-gray-200 dark:ring-gray-800 rounded-lg overflow-hidden',
                thead: 'bg-gradient-to-r from-green-50 to-emerald-50 dark:from-green-900/20 dark:to-emerald-900/20',
                tbody: 'divide-y divide-gray-200 dark:divide-gray-800',
                th: 'py-4 px-4 text-left font-bold text-gray-900 dark:text-white',
                td: 'py-4 px-4'
              }"
            />
          </div>

          <!-- Leyenda de Rates -->
          <div class="mt-4 p-3 bg-green-50 dark:bg-green-900/20 rounded-lg h-auto">
            <div class="flex flex-wrap gap-4 text-sm">
              <div class="flex items-center gap-2">
                <div class="w-3 h-3 bg-green-500 rounded"></div>
                <span class="text-gray-600 dark:text-gray-400">Experiencias</span>
              </div>
              <div class="flex items-center gap-2">
                <div class="w-3 h-3 bg-red-500 rounded"></div>
                <span class="text-gray-600 dark:text-gray-400">Porcentajes</span>
              </div>
            </div>
          </div>
        </UCard>

        <!-- Tabla de NPCs -->
        <UCard class="h-fit">
          <template #header>
            <div class="flex items-center justify-between">
              <div>
                <h2 class="text-2xl font-bold text-gray-900 dark:text-white flex items-center gap-2">
                  <UIcon name="i-heroicons-user-group" class="text-blue-500" />
                  NPCs Disponibles
                </h2>
                <p class="text-gray-600 dark:text-gray-400 mt-1">Algunos servicios y funcionalidades dentro del servidor.</p>
              </div>
              <UBadge color="blue" variant="solid">
                {{ npcsData.length }} NPCs
              </UBadge>
            </div>
          </template>

          <div class="overflow-x-auto">
            <UTable 
              :data="npcsData" 
              :columns="npcsColumns" 
              :ui="{
                wrapper: 'ring-1 ring-gray-200 dark:ring-gray-800 rounded-lg overflow-hidden',
                thead: 'bg-gradient-to-r from-blue-50 to-cyan-50 dark:from-blue-900/20 dark:to-cyan-900/20',
                tbody: 'divide-y divide-gray-200 dark:divide-gray-800',
                th: 'py-4 px-4 text-left font-bold text-gray-900 dark:text-white',
                td: 'py-4 px-4'
              }"
            />
          </div>

          <!-- Estadísticas de NPCs -->
          <div class="mt-4 grid grid-cols-2 gap-2 text-sm">
            <div class="text-center p-2 bg-blue-50 dark:bg-blue-900/20 rounded">
              <div class="font-bold text-blue-600 dark:text-blue-400">{{ npcsData.length }}</div>
              <div class="text-gray-600 dark:text-gray-400">Total NPCs</div>
            </div>
            <div class="text-center p-2 bg-blue-50 dark:bg-blue-900/20 rounded">
              <div class="font-bold text-blue-600 dark:text-blue-400">8+</div>
              <div class="text-gray-600 dark:text-gray-400">Servicios</div>
            </div>
          </div>
        </UCard>
      </div>

      <!-- Sección de características -->
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 mb-12">
        <!-- Características principales -->
        <UCard>
          <template #header>
            <h3 class="text-xl font-bold text-gray-900 dark:text-white flex items-center gap-2">
              <UIcon name="i-heroicons-star" class="text-yellow-500" />
              Características Principales
            </h3>
          </template>
          <div class="space-y-4">
            <div v-for="feature in [
              'Sistema de Random Options avanzado',
              'Skills balanceados y mejorados',
              'Sistema de PvP/GvG completo',
              'NPCs de utilidad mejorados',
              'Sistema de refinamiento clásico',
              'Comandos personalizados Xtreme Pixel'
            ]" :key="feature" class="flex items-center gap-3">
              <UIcon name="i-heroicons-check-circle" class="text-green-500 flex-shrink-0" />
              <span class="text-gray-700 dark:text-gray-300">{{ feature }}</span>
            </div>
          </div>
        </UCard>

        <!-- Información de contacto -->
        <UCard>
          <template #header>
            <h3 class="text-xl font-bold text-gray-900 dark:text-white flex items-center gap-2">
              <UIcon name="i-heroicons-information-circle" class="text-blue-500" />
              Conéctate con Nosotros
            </h3>
          </template>
          <div class="space-y-4">
            <div class="flex items-center gap-3 p-3 bg-gradient-to-r from-blue-50 to-purple-50 dark:from-blue-900/20 dark:to-purple-900/20 rounded-lg">
              <UIcon name="i-simple-icons-discord" class="text-indigo-500 text-xl" />
              <div>
                <div class="font-semibold text-gray-900 dark:text-white">Discord Oficial</div>
                <div class="text-sm text-gray-600 dark:text-gray-400">Únete a nuestra comunidad</div>
              </div>
            </div>
            <div class="flex items-center gap-3 p-3 bg-gradient-to-r from-green-50 to-emerald-50 dark:from-green-900/20 dark:to-emerald-900/20 rounded-lg">
              <UIcon name="i-heroicons-document-text" class="text-green-500 text-xl" />
              <div>
                <div class="font-semibold text-gray-900 dark:text-white">Servidor de Calidad</div>
                <div class="text-sm text-gray-600 dark:text-gray-400">Sin Administración Bananera</div>
              </div>
            </div>
            <div class="flex items-center gap-3 p-3 bg-gradient-to-r from-red-50 to-orange-50 dark:from-red-900/20 dark:to-orange-900/20 rounded-lg">
              <UIcon name="material-symbols-light-diamond-outline-rounded" class="text-red-500 text-xl" />
              <div>
                <div class="font-semibold text-gray-900 dark:text-white">Servidor 100% libre de corrupción</div>
                <div class="text-sm text-gray-600 dark:text-gray-400">No RTM</div>
              </div>
            </div>
          </div>
        </UCard>
      </div>

      <!-- Call to Action -->
      <div class="text-center mt-16 p-8 bg-gradient-to-r from-purple-500 to-blue-600 rounded-2xl text-white shadow-xl">
        <h2 class="text-3xl font-bold mb-4">¿Listo para la Aventura?</h2>
        <p class="text-xl mb-6 text-purple-100">
          Únete a cientos de jugadores en este servidor clásico de Ragnarok Online
        </p>
        <div class="flex flex-col sm:flex-row gap-4 justify-center">
          <UButton 
            size="xl" 
            color="white" 
            variant="solid"
            class="font-bold text-purple-600 hover:scale-105 transition-transform"
            href="https://discord.gg/66f3ZfPKBY"
            target="_blank"
          >
            Únete a la Comunidad
          </UButton>
        </div>
      </div>
    </UContainer>
  </div>
</template>