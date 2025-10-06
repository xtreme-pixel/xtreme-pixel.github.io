<script setup lang="ts">
import { h } from 'vue'
import type { TableColumn } from '@nuxt/ui'

useHead({
  title: 'Refine',
  meta: [
    { name: 'description', content: 'Rates de refinamiento Xtreme Pixel' }
  ]
})

type RefinementData = {
  equipment: string
  plus1: string
  plus2: string
  plus3: string
  plus4: string
  plus5: string
  plus6: string
  plus7: string
  plus8: string
  plus9: string
  plus10: string
}

const refinementData = ref<RefinementData[]>([
  {
    equipment: 'Weapon Lv 1',
    plus1: '100%',
    plus2: '100%',
    plus3: '100%',
    plus4: '100%',
    plus5: '100%',
    plus6: '100%',
    plus7: '100%',
    plus8: '60%',
    plus9: '40%',
    plus10: '19%'
  },
  {
    equipment: 'Weapon Lv 2',
    plus1: '100%',
    plus2: '100%',
    plus3: '100%',
    plus4: '100%',
    plus5: '100%',
    plus6: '100%',
    plus7: '60%',
    plus8: '40%',
    plus9: '20%',
    plus10: '19%'
  },
  {
    equipment: 'Weapon Lv 3',
    plus1: '100%',
    plus2: '100%',
    plus3: '100%',
    plus4: '100%',
    plus5: '100%',
    plus6: '60%',
    plus7: '50%',
    plus8: '20%',
    plus9: '20%',
    plus10: '19%'
  },
  {
    equipment: 'Weapon Lv 4',
    plus1: '100%',
    plus2: '100%',
    plus3: '100%',
    plus4: '100%',
    plus5: '60%',
    plus6: '40%',
    plus7: '40%',
    plus8: '20%',
    plus9: '20%',
    plus10: '9%'
  },
  {
    equipment: 'Armor',
    plus1: '100%',
    plus2: '100%',
    plus3: '100%',
    plus4: '100%',
    plus5: '60%',
    plus6: '40%',
    plus7: '40%',
    plus8: '20%',
    plus9: '20%',
    plus10: '9%'
  }
])

// Estadísticas de refinamiento
const refinementStats = ref({
  totalEquipment: '5 tipos',
  maxSuccessRate: '100%',
  minSuccessRate: '9%',
  lastUpdated: 'Septiembre 2025'
})

const columns: TableColumn<RefinementData>[] = [
  {
    accessorKey: 'equipment',
    header: 'Equipment',
    cell: ({ row }) => h('div', { 
      class: 'font-bold text-gray-900 dark:text-white text-sm' 
    }, row.getValue('equipment'))
  },
  {
    accessorKey: 'plus1',
    header: '+1',
    cell: ({ row }) => createRefinementCell(row.getValue('plus1'))
  },
  {
    accessorKey: 'plus2',
    header: '+2',
    cell: ({ row }) => createRefinementCell(row.getValue('plus2'))
  },
  {
    accessorKey: 'plus3',
    header: '+3',
    cell: ({ row }) => createRefinementCell(row.getValue('plus3'))
  },
  {
    accessorKey: 'plus4',
    header: '+4',
    cell: ({ row }) => createRefinementCell(row.getValue('plus4'))
  },
  {
    accessorKey: 'plus5',
    header: '+5',
    cell: ({ row }) => createRefinementCell(row.getValue('plus5'))
  },
  {
    accessorKey: 'plus6',
    header: '+6',
    cell: ({ row }) => createRefinementCell(row.getValue('plus6'))
  },
  {
    accessorKey: 'plus7',
    header: '+7',
    cell: ({ row }) => createRefinementCell(row.getValue('plus7'))
  },
  {
    accessorKey: 'plus8',
    header: '+8',
    cell: ({ row }) => createRefinementCell(row.getValue('plus8'))
  },
  {
    accessorKey: 'plus9',
    header: '+9',
    cell: ({ row }) => createRefinementCell(row.getValue('plus9'))
  },
  {
    accessorKey: 'plus10',
    header: '+10',
    cell: ({ row }) => createRefinementCell(row.getValue('plus10'))
  }
]

function createRefinementCell(value: string) {
  const percentage = value.replace('%', '')
  const numericValue = parseInt(percentage)
  
  let colorClass = ''
  if (numericValue === 100) {
    colorClass = 'text-green-600 dark:text-green-400 bg-green-50 dark:bg-green-900/20'
  } else if (numericValue >= 40) {
    colorClass = 'text-blue-600 dark:text-blue-400 bg-blue-50 dark:bg-blue-900/20'
  } else if (numericValue >= 20) {
    colorClass = 'text-orange-600 dark:text-orange-400 bg-orange-50 dark:bg-orange-900/20'
  } else {
    colorClass = 'text-red-600 dark:text-red-400 bg-red-50 dark:bg-red-900/20'
  }

  return h('div', {
    class: `text-center font-semibold py-1 px-2 rounded-lg ${colorClass}`
  }, value)
}
</script>

<template>
  <div class="min-h-screen bg-gradient-to-br from-blue-50 to-indigo-100 dark:from-gray-900 dark:to-blue-900">
    <!-- Header Hero -->
    <div class="relative bg-gradient-to-r from-purple-600 via-blue-600 to-indigo-700 text-white py-16">
      <div class="absolute inset-0 bg-black/20"></div>
      <UContainer class="relative z-10">
        <div class="text-center">
          <h1 class="text-4xl font-bold mb-4 bg-gradient-to-r from-yellow-300 to-orange-300 bg-clip-text text-transparent">
            Sistema de Refinamiento
          </h1>
          <p class="text-xl mb-6 text-blue-100">
            Probabilidades de éxito para el refinamiento de equipamiento
          </p>
          <div class="inline-flex items-center gap-4 bg-white/10 backdrop-blur-sm px-6 py-3 rounded-full">
            <UIcon name="i-heroicons-chart-bar" class="text-yellow-300" />
            <span class="text-sm">Actualizado: {{ refinementStats.lastUpdated }}</span>
            <span class="text-sm">•</span>
            <span class="text-sm">{{ refinementStats.totalEquipment }} de equipos</span>
          </div>
        </div>
      </UContainer>
    </div>

    <UContainer class="py-12">
      <!-- Tarjetas de estadísticas -->
      <div class="grid grid-cols-1 md:grid-cols-4 gap-6 mb-12">
        <UCard class="text-center bg-white/80 dark:bg-gray-800/80 backdrop-blur-sm">
          <template #header>
            <h3 class="text-lg font-semibold text-gray-900 dark:text-white">Tipos de Equipo</h3>
          </template>
          <div class="text-3xl font-bold text-purple-600 dark:text-purple-400">
            {{ refinementStats.totalEquipment }}
          </div>
          <p class="text-sm text-gray-600 dark:text-gray-400 mt-2">Armas y Armaduras</p>
        </UCard>

        <UCard class="text-center bg-white/80 dark:bg-gray-800/80 backdrop-blur-sm">
          <template #header>
            <h3 class="text-lg font-semibold text-gray-900 dark:text-white">Máxima Probabilidad</h3>
          </template>
          <div class="text-3xl font-bold text-green-600 dark:text-green-400">
            {{ refinementStats.maxSuccessRate }}
          </div>
          <p class="text-sm text-gray-600 dark:text-gray-400 mt-2">Refinamiento seguro</p>
        </UCard>

        <UCard class="text-center bg-white/80 dark:bg-gray-800/80 backdrop-blur-sm">
          <template #header>
            <h3 class="text-lg font-semibold text-gray-900 dark:text-white">Mínima Probabilidad</h3>
          </template>
          <div class="text-3xl font-bold text-red-600 dark:text-red-400">
            {{ refinementStats.minSuccessRate }}
          </div>
          <p class="text-sm text-gray-600 dark:text-gray-400 mt-2">Refinamiento arriesgado</p>
        </UCard>

        <UCard class="text-center bg-white/80 dark:bg-gray-800/80 backdrop-blur-sm">
          <template #header>
            <h3 class="text-lg font-semibold text-gray-900 dark:text-white">Niveles</h3>
          </template>
          <div class="text-3xl font-bold text-blue-600 dark:text-blue-400">
            +1 a +10
          </div>
          <p class="text-sm text-gray-600 dark:text-gray-400 mt-2">Niveles de refinamiento</p>
        </UCard>
      </div>

      <!-- Tabla de Refinamiento -->
      <UCard class="mb-12">
        <template #header>
          <div class="flex items-center justify-between">
            <div>
              <h2 class="text-2xl font-bold text-gray-900 dark:text-white flex items-center gap-2">
                <UIcon name="i-heroicons-wrench-screwdriver" class="text-orange-500" />
                Tasas de Refinamiento
              </h2>
              <p class="text-gray-600 dark:text-gray-400 mt-1">
                Probabilidades de éxito por nivel y tipo de equipo
              </p>
            </div>
            <UBadge color="orange" variant="solid" size="lg">
              {{ refinementData.length }} Equipos
            </UBadge>
          </div>
        </template>

        <div class="overflow-x-auto">
          <UTable 
            :data="refinementData" 
            :columns="columns" 
            class="flex-1 min-w-max"
            :ui="{
              wrapper: 'ring-1 ring-gray-200 dark:ring-gray-800 rounded-lg overflow-hidden',
              thead: 'bg-gradient-to-r from-orange-50 to-amber-50 dark:from-orange-900/20 dark:to-amber-900/20',
              tbody: 'divide-y divide-gray-200 dark:divide-gray-800',
              th: 'py-4 px-3 text-center font-bold text-gray-900 dark:text-white whitespace-nowrap',
              td: 'py-3 px-3'
            }"
          />
        </div>

        <!-- Leyenda de colores -->
        <div class="mt-6 p-4 bg-orange-50 dark:bg-orange-900/20 rounded-lg">
          <h4 class="font-semibold text-gray-900 dark:text-white mb-3 flex items-center gap-2">
            <UIcon name="i-heroicons-key" class="text-orange-500" />
            Leyenda de Probabilidades
          </h4>
          <div class="flex flex-wrap gap-4 text-sm">
            <div class="flex items-center gap-2">
              <div class="w-3 h-3 bg-green-500 rounded"></div>
              <span class="text-gray-600 dark:text-gray-400">100% Success</span>
            </div>
            <div class="flex items-center gap-2">
              <div class="w-3 h-3 bg-blue-500 rounded"></div>
              <span class="text-gray-600 dark:text-gray-400">40%-99% Success</span>
            </div>
            <div class="flex items-center gap-2">
              <div class="w-3 h-3 bg-orange-500 rounded"></div>
              <span class="text-gray-600 dark:text-gray-400">20%-39% Success</span>
            </div>
            <div class="flex items-center gap-2">
              <div class="w-3 h-3 bg-red-500 rounded"></div>
              <span class="text-gray-600 dark:text-gray-400">Below 20% Success</span>
            </div>
          </div>
        </div>
      </UCard>

      <!-- Información Adicional -->
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 mb-12">
        <!-- Consejos de Refinamiento -->
        <UCard>
          <template #header>
            <h3 class="text-xl font-bold text-gray-900 dark:text-white flex items-center gap-2">
              <UIcon name="i-heroicons-light-bulb" class="text-yellow-500" />
              Consejos de Refinamiento
            </h3>
          </template>
          <div class="space-y-4">
            <div v-for="tip in [
              'Refina hasta +7 con seguridad en la mayoría de equipos',
              'Usa oridecones y eluniums para mejores resultados',
              'Considera usar NPC de protección para refinamientos altos',
              'Las armas nivel 4 son las más difíciles de refinar',
              'El equipamiento no pierde Random Option al refinarse'
            ]" :key="tip" class="flex items-start gap-3">
              <UIcon name="i-heroicons-sparkles" class="text-blue-500 flex-shrink-0 mt-0.5" />
              <span class="text-gray-700 dark:text-gray-300 text-sm leading-relaxed">{{ tip }}</span>
            </div>
          </div>
        </UCard>

        <!-- Estadísticas Rápidas -->
        <UCard>
          <template #header>
            <h3 class="text-xl font-bold text-gray-900 dark:text-white flex items-center gap-2">
              <UIcon name="i-heroicons-chart-pie" class="text-green-500" />
              Datos Importantes
            </h3>
          </template>
          <div class="space-y-3">
            <div class="flex justify-between items-center py-2 border-b border-gray-200 dark:border-gray-700">
              <span class="text-gray-600 dark:text-gray-400">Equipos con 100% hasta +7:</span>
              <UBadge color="green" variant="subtle">3 tipos</UBadge>
            </div>
            <div class="flex justify-between items-center py-2 border-b border-gray-200 dark:border-gray-700">
              <span class="text-gray-600 dark:text-gray-400">Refinamiento más seguro:</span>
              <UBadge color="blue" variant="subtle">Weapon Lv 1</UBadge>
            </div>
            <div class="flex justify-between items-center py-2 border-b border-gray-200 dark:border-gray-700">
              <span class="text-gray-600 dark:text-gray-400">Refinamiento más arriesgado:</span>
              <UBadge color="red" variant="subtle">Weapon Lv 4 +10</UBadge>
            </div>
            <div class="flex justify-between items-center py-2">
              <span class="text-gray-600 dark:text-gray-400">Nivel crítico general:</span>
              <UBadge color="orange" variant="subtle">+8</UBadge>
            </div>
          </div>
        </UCard>
      </div>

      <!-- Call to Action -->
      <div class="text-center p-8 bg-gradient-to-r from-orange-500 to-amber-600 rounded-2xl text-white shadow-xl">
        <h2 class="text-3xl font-bold mb-4">¿Necesitas Materiales?</h2>
        <p class="text-xl mb-6 text-orange-100">
          El Tool Dealer en el apartado de Refining vende lo necesario
        </p>
        <div class="flex flex-col sm:flex-row gap-4 justify-center">
          <UButton 
            size="xl" 
            color="gray" 
            variant="outline"
            class="font-bold border-white text-white hover:bg-white hover:text-orange-600 transition-all"
            href="https://discord.gg/66f3ZfPKBY"
            target="_blank"
          >
            <UIcon name="i-heroicons-question-mark-circle" class="w-5 h-5" />
            Consulta en Discord, para mas dudas
          </UButton>
        </div>
      </div>
    </UContainer>
  </div>
</template>