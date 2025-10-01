<script setup lang="ts">
import { h } from 'vue'
import type { TableColumn } from '@nuxt/ui'

useHead({
  title: 'Habilidades',
  meta: [
    { name: 'description', content: 'Habilidades mejoradas Xtreme Pixel - Sistema único de balance' }
  ]
})

type Skill = {
  skill: string
  edit: string
  type: string
  class: string
}

const skillsData = ref<Skill[]>([
  { skill: 'Blessing', edit: 'Bonus incrementado 3 veces', type: 'No afecta a usables o NPC', class: 'Acolyte' },
  { skill: 'AGI', edit: 'Bonus incrementado 3 veces', type: 'No afecta a usables o NPC', class: 'Acolyte' },
  { skill: 'Heal', edit: 'Bonus incrementado 3 veces', type: 'No afecta a usables o NPC', class: 'Acolyte' },
  { skill: 'Holy Light', edit: 'Se aumenta a 2 hits', type: '', class: 'Acolyte' },
  { skill: 'Finger Offensive', edit: 'Utiliza una esfera', type: '', class: 'Champion' },
  { skill: 'Slim Potion Pitcher', edit: 'Bonus incrementado 3 veces', type: '', class: 'Creator' },
  { skill: 'Potion Pitcher', edit: 'Bonus incrementado 3 veces', type: '', class: 'Creator' },
  { skill: 'Crazy Uproar', edit: 'Ahora da 12 de STR', type: '', class: 'Merchant' },
  { skill: 'Sanctuary', edit: 'Bonus incrementado 3 veces', type: '', class: 'Priest' },
  { skill: 'Gloria', edit: 'Bonus incrementado 3 veces', type: '', class: 'Priest' },
  { skill: 'Impositio', edit: 'Bonus incrementado 3 veces', type: '', class: 'Priest' },
  { skill: 'Full Strip', edit: 'Bypass FCP, misma formula con un 50% de chance, requiere Rogue Link + Glistening coat', type: '', class: 'Stalker' },
  { skill: 'Back Stap', edit: 'Ya no depende de estar detras del enemigo y su daño incrementa con dagas', type: '', class: 'Stalker' },
  { skill: 'Provoke', edit: 'Funciona en aliados', type: '', class: 'Swordman' },
  { skill: 'Mind Braker', edit: 'Funciona en aliados', type: '', class: 'Professor' },
  { skill: 'Grimtooth', edit: 'Rango aumentado a 9', type: '', class: 'Assassin' },
  { skill: 'Mammonite', edit: 'Costo eliminado', type: '', class: 'Merchant' },
  { skill: 'Cart Terminator', edit: 'Costo eliminado', type: '', class: 'Withesmith' },
  { skill: 'Land Protector', edit: 'Funcionamiento Old School', type: '', class: 'Professor' },
  { skill: 'Meteor Storm', edit: 'Funcionamiento Old School', type: '', class: 'Wizard' },
  { skill: 'Storm Gust', edit: 'Funcionamiento Old School', type: '', class: 'Wizard' },
  { skill: 'Lord of Vermillion', edit: 'Funcionamiento Old School', type: '', class: 'Wizard' }
])

// CORRECCIÓN: Acceder a .value para las estadísticas
const skillsStats = ref({
  totalSkills: skillsData.value.length,
  uniqueClasses: new Set(skillsData.value.map(s => s.class)).size,
  buffedSkills: skillsData.value.filter(s => s.edit.includes('incrementado') || s.edit.includes('aumentado')).length,
  reworkedSkills: skillsData.value.filter(s => s.edit.includes('Funcionamiento') || s.edit.includes('eliminado')).length
})

const columns: TableColumn<Skill>[] = [
  {
    accessorKey: 'skill',
    header: 'Skill',
    cell: ({ row }) => h('div', { 
      class: 'font-bold text-gray-900 dark:text-white text-sm' 
    }, row.getValue('skill'))
  },
  {
    accessorKey: 'edit',
    header: 'Mejora',
    cell: ({ row }) => {
      const edit = row.getValue('edit') as string
      return h('div', { 
        class: 'text-green-600 dark:text-green-400 text-sm leading-tight' 
      }, edit)
    }
  },
  {
    accessorKey: 'type',
    header: 'Tipo',
    cell: ({ row }) => {
      const type = row.getValue('type') as string
      if (!type) return h('div', { class: 'text-gray-400 text-sm italic' }, 'Sin restricciones')
      
      return h('div', { 
        class: 'text-orange-600 dark:text-orange-400 text-sm italic' 
      }, type)
    }
  },
  {
    accessorKey: 'class',
    header: 'Job',
    cell: ({ row }) => {
      const className = row.getValue('class') as string
      const colorClass = {
        'Acolyte': 'bg-blue-100 text-blue-800 dark:bg-blue-900 dark:text-blue-300',
        'Champion': 'bg-yellow-100 text-yellow-800 dark:bg-yellow-900 dark:text-yellow-300',
        'Creator': 'bg-green-100 text-green-800 dark:bg-green-900 dark:text-green-300',
        'Merchant': 'bg-orange-100 text-orange-800 dark:bg-orange-900 dark:text-orange-300',
        'Priest': 'bg-purple-100 text-purple-800 dark:bg-purple-900 dark:text-purple-300',
        'Stalker': 'bg-red-100 text-red-800 dark:bg-red-900 dark:text-red-300',
        'Swordman': 'bg-gray-100 text-gray-800 dark:bg-gray-900 dark:text-gray-300',
        'Professor': 'bg-indigo-100 text-indigo-800 dark:bg-indigo-900 dark:text-indigo-300',
        'Assassin': 'bg-gray-800 text-white dark:bg-gray-600 dark:text-white',
        'Withesmith': 'bg-amber-100 text-amber-800 dark:bg-amber-900 dark:text-amber-300',
        'Wizard': 'bg-cyan-100 text-cyan-800 dark:bg-cyan-900 dark:text-cyan-300'
      }[className] || 'bg-gray-100 text-gray-800 dark:bg-gray-900 dark:text-gray-300'

      return h('span', { 
        class: `inline-flex items-center px-2.5 py-1 rounded-full text-xs font-bold ${colorClass}`
      }, className)
    }
  }
]

// Filtrar por clase
const selectedClass = ref('Todas')
const classes = ['Todas', 'Acolyte', 'Champion', 'Creator', 'Merchant', 'Priest', 'Stalker', 'Swordman', 'Professor', 'Assassin', 'Withesmith', 'Wizard']

const filteredSkills = computed(() => {
  if (selectedClass.value === 'Todas') {
    return skillsData.value
  }
  return skillsData.value.filter(skill => skill.class === selectedClass.value)
})

// CORRECCIÓN: Función para contar habilidades por clase
const getSkillsCountByClass = (classType: string) => {
  return skillsData.value.filter(skill => skill.class === classType).length
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
            Habilidades Mejoradas
          </h1>
          <p class="text-xl mb-6 text-blue-100">
            Sistema único de balance y mejoras para una experiencia de juego optimizada
          </p>
          <div class="inline-flex items-center gap-4 bg-white/10 backdrop-blur-sm px-6 py-3 rounded-full">
            <UIcon name="i-heroicons-sparkles" class="text-yellow-300" />
            <span class="text-sm">{{ skillsStats.totalSkills }} habilidades mejoradas</span>
            <span class="text-sm">•</span>
            <span class="text-sm">{{ skillsStats.uniqueClasses }} clases únicas</span>
          </div>
        </div>
      </UContainer>
    </div>

    <UContainer class="py-12">
      <!-- Tarjetas de estadísticas -->
      <div class="grid grid-cols-1 md:grid-cols-4 gap-6 mb-12">
        <UCard class="text-center bg-white/80 dark:bg-gray-800/80 backdrop-blur-sm">
          <template #header>
            <h3 class="text-lg font-semibold text-gray-900 dark:text-white">Total Mejoradas</h3>
          </template>
          <div class="text-3xl font-bold text-purple-600 dark:text-purple-400">
            {{ skillsStats.totalSkills }}
          </div>
          <p class="text-sm text-gray-600 dark:text-gray-400 mt-2">Habilidades modificadas</p>
        </UCard>

        <UCard class="text-center bg-white/80 dark:bg-gray-800/80 backdrop-blur-sm">
          <template #header>
            <h3 class="text-lg font-semibold text-gray-900 dark:text-white">Clases Únicas</h3>
          </template>
          <div class="text-3xl font-bold text-blue-600 dark:text-blue-400">
            {{ skillsStats.uniqueClasses }}
          </div>
          <p class="text-sm text-gray-600 dark:text-gray-400 mt-2">Jobs beneficiados</p>
        </UCard>

        <UCard class="text-center bg-white/80 dark:bg-gray-800/80 backdrop-blur-sm">
          <template #header>
            <h3 class="text-lg font-semibold text-gray-900 dark:text-white">Habilidades Buffed</h3>
          </template>
          <div class="text-3xl font-bold text-green-600 dark:text-green-400">
            {{ skillsStats.buffedSkills }}
          </div>
          <p class="text-sm text-gray-600 dark:text-gray-400 mt-2">Mejoras de poder</p>
        </UCard>

        <UCard class="text-center bg-white/80 dark:bg-gray-800/80 backdrop-blur-sm">
          <template #header>
            <h3 class="text-lg font-semibold text-gray-900 dark:text-white">Reworkeadas</h3>
          </template>
          <div class="text-3xl font-bold text-orange-600 dark:text-orange-400">
            {{ skillsStats.reworkedSkills }}
          </div>
          <p class="text-sm text-gray-600 dark:text-gray-400 mt-2">Mecánicas cambiadas</p>
        </UCard>
      </div>

      <!-- Filtros por clase -->
      <UCard class="mb-6">
        <template #header>
          <div class="flex items-center justify-between">
            <div>
              <h3 class="text-lg font-semibold text-gray-900 dark:text-white mb-1">
                Filtrar por Clase
              </h3>
              <p class="text-sm text-gray-600 dark:text-gray-400">
                Explora las mejoras específicas de cada job
              </p>
            </div>
            <UBadge color="blue" variant="subtle">
              {{ filteredSkills.length }} mostradas
            </UBadge>
          </div>
        </template>
        <div class="flex flex-wrap gap-2">
          <UButton
            v-for="classType in classes"
            :key="classType"
            :color="selectedClass === classType ? 'primary' : 'gray'"
            variant="solid"
            @click="selectedClass = classType"
            class="mb-2"
            size="sm"
          >
            {{ classType }}
            <template v-if="classType !== 'Todas'">
              <span class="ml-1 bg-white/20 px-1.5 py-0.5 rounded text-xs">
                {{ getSkillsCountByClass(classType) }}
              </span>
            </template>
          </UButton>
        </div>
      </UCard>

      <!-- Tabla de Habilidades -->
      <UCard class="mb-12">
        <template #header>
          <div class="flex items-center justify-between">
            <div>
              <h2 class="text-2xl font-bold text-gray-900 dark:text-white flex items-center gap-2">
                <UIcon name="i-heroicons-wrench-screwdriver" class="text-green-500" />
                Lista de Habilidades Mejoradas
              </h2>
              <p class="text-gray-600 dark:text-gray-400 mt-1">
                Habilidades que han sido modificadas con respecto al servidor oficial para mejor balance y jugabilidad
              </p>
            </div>
            <UBadge color="green" variant="solid" size="lg">
              {{ filteredSkills.length }} Skills
            </UBadge>
          </div>
        </template>

        <div class="overflow-x-auto">
          <UTable 
            :data="filteredSkills" 
            :columns="columns" 
            class="flex-1 min-w-max"
            :ui="{
              wrapper: 'ring-1 ring-gray-200 dark:ring-gray-800 rounded-lg overflow-hidden',
              thead: 'bg-gradient-to-r from-green-50 to-emerald-50 dark:from-green-900/20 dark:to-emerald-900/20',
              tbody: 'divide-y divide-gray-200 dark:divide-gray-800',
              th: 'py-4 px-4 text-left font-bold text-gray-900 dark:text-white whitespace-nowrap',
              td: 'py-3 px-4'
            }"
          />
        </div>

        <!-- Leyenda e Información -->
        <div class="mt-6 grid grid-cols-1 lg:grid-cols-2 gap-4">
          <div class="p-4 bg-green-50 dark:bg-green-900/20 rounded-lg">
            <h4 class="font-semibold text-green-800 dark:text-green-300 mb-3 flex items-center gap-2">
              <UIcon name="i-heroicons-key" class="text-green-500" />
              Leyenda de Mejoras
            </h4>
            <div class="space-y-2 text-sm">
              <div class="flex items-center gap-2">
                <div class="w-3 h-3 bg-green-500 rounded"></div>
                <span class="text-gray-600 dark:text-gray-400">Mejora: Modificación aplicada a la skill</span>
              </div>
              <div class="flex items-center gap-2">
                <div class="w-3 h-3 bg-orange-500 rounded"></div>
                <span class="text-gray-600 dark:text-gray-400">Tipo: Restricciones o condiciones especiales</span>
              </div>
            </div>
          </div>
          <div class="p-4 bg-blue-50 dark:bg-blue-900/20 rounded-lg">
            <h4 class="font-semibold text-blue-800 dark:text-blue-300 mb-2 flex items-center gap-2">
              <UIcon name="i-heroicons-information-circle" class="text-blue-500" />
              Tipos de Mejoras
            </h4>
            <ul class="text-blue-700 dark:text-blue-400 text-sm space-y-1">
              <li>• <strong>Bonus Incrementado:</strong> Aumento en potencia o duración</li>
              <li>• <strong>Mecánica Cambiada:</strong> Nuevo funcionamiento</li>
              <li>• <strong>Costo Eliminado:</strong> Sin consumo de recursos</li>
              <li>• <strong>Old School:</strong> Comportamiento clásico</li>
            </ul>
          </div>
        </div>
      </UCard>

      <!-- Sección de Mejoras Destacadas -->
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 mb-12">
        <!-- Mejoras de Soporte -->
        <UCard>
          <template #header>
            <h3 class="text-xl font-bold text-gray-900 dark:text-white flex items-center gap-2">
              <UIcon name="i-heroicons-heart" class="text-red-500" />
              Mejoras de Soporte
            </h3>
          </template>
          <div class="space-y-4">
            <div v-for="improvement in [
              'Blessing, AGI, Heal: Bonus incrementado 3 veces',
              'Sanctuary, Gloria, Impositio: Buffs potenciados',
              'Provoke, Mind Braker: Ahora funcionan en aliados',
              'Potion Pitcher: Curación masiva incrementada'
            ]" :key="improvement" class="flex items-start gap-3">
              <UIcon name="i-heroicons-check-badge" class="text-green-500 flex-shrink-0 mt-0.5" />
              <span class="text-gray-700 dark:text-gray-300 text-sm leading-relaxed">{{ improvement }}</span>
            </div>
          </div>
        </UCard>

        <!-- Mejoras de Daño -->
        <UCard>
          <template #header>
            <h3 class="text-xl font-bold text-gray-900 dark:text-white flex items-center gap-2">
              <UIcon name="i-heroicons-bolt" class="text-yellow-500" />
              Mejoras Ofensivas
            </h3>
          </template>
          <div class="space-y-4">
            <div v-for="improvement in [
              'Holy Light: Ahora realiza 2 hits',
              'Grimtooth: Rango aumentado a 9 celdas',
              'Meteor Storm, Storm Gust: Funcionamiento Old School, Stack en Land',
              'Back Stab: Daño aumentado y mayor facilidad'
            ]" :key="improvement" class="flex items-start gap-3">
              <UIcon name="i-heroicons-fire" class="text-orange-500 flex-shrink-0 mt-0.5" />
              <span class="text-gray-700 dark:text-gray-300 text-sm leading-relaxed">{{ improvement }}</span>
            </div>
          </div>
        </UCard>
      </div>

      <!-- Call to Action -->
      <div class="text-center p-8 bg-gradient-to-r from-green-500 to-emerald-600 rounded-2xl text-white shadow-xl">
        <h2 class="text-3xl font-bold mb-4">¿Listo para Probar las Mejoras?</h2>
        <p class="text-xl mb-6 text-green-100">
          Descubre cómo estas mejoras transforman la experiencia de juego en Xtreme Pixel
        </p>
        <div class="flex flex-col sm:flex-row gap-4 justify-center">
          <UButton 
            size="xl" 
            color="gray" 
            variant="outline"
            class="font-bold border-white text-white hover:bg-white hover:text-green-600 transition-all"
            to="/download"
          >
            <UIcon name="i-heroicons-book-open" class="w-5 h-5" />
            Descargar Cliente
          </UButton>
        </div>
      </div>
    </UContainer>
  </div>
</template>