<script setup lang="ts">
import { h } from 'vue'
import type { TableColumn } from '@nuxt/ui'

useHead({
  title: 'Comandos',
  meta: [
    { name: 'description', content: 'Lista completa de comandos disponibles en Xtreme Pixel RO' }
  ]
})

type Command = {
  command: string
  description: string
  category: string
}

const commandsData = ref<Command[]>([
  // Social & Party Commands
  { command: 'changedress', description: 'Remueve los cosplay de los personajes', category: 'Social' },
  { command: 'listenbg', description: 'Activa/desactiva los mensajes de BG', category: 'Social' },
  { command: 'guildskill', description: 'Permite usar habilidades del gremio', category: 'Social' },
  { command: 'order', description: 'Da órdenes a los miembros de BG', category: 'Social' },
  { command: 'reportafk', description: 'Reporta jugadores que están AFK (Away From Keyboard) en BG', category: 'Social' },
  { command: 'leader', description: 'Comandos exclusivos para el líder de BG, permite transferir el lider', category: 'Social' },
  { command: 'vote', description: 'Inicia una votación en BG', category: 'Social' },
  { command: 'votekick', description: 'Vota para expulsar a un jugador de BG', category: 'Social' },
  { command: 'voteleader', description: 'Vota para cambiar al líder', category: 'Social' },
  { command: 'duel', description: 'Inicia un duelo PvP con otro jugador', category: 'Social' },
  { command: 'leave', description: 'Abandona el duelo', category: 'Social' },
  { command: 'accept', description: 'Acepta una solicitud de duelo', category: 'Social' },
  { command: 'reject', description: 'Rechaza una solicitud de duelo', category: 'Social' },

  // Informational Commands
  { command: 'commands', description: 'Muestra la lista de comandos disponibles', category: 'Información' },
  { command: 'charcommands', description: 'Muestra comandos específicos del personaje', category: 'Información' },
  { command: 'help', description: 'Muestra ayuda sobre comandos específicos', category: 'Información' },
  { command: 'rates', description: 'Muestra las tasas de experiencia y drop del servidor', category: 'Información' },
  { command: 'uptime', description: 'Muestra el tiempo que el servidor ha estado activo', category: 'Información' },
  { command: 'showdelay', description: 'Muestra los errores de utilizar habilidad', category: 'Información' },
  { command: 'exp', description: 'Muestra la experiencia actual y el nivel', category: 'Información' },
  { command: 'mobinfo', description: 'Muestra información sobre un monstruo específico', category: 'Información' },
  { command: 'iteminfo', description: 'Muestra información detallada de un item', category: 'Información' },
  { command: 'whodrops', description: 'Muestra qué monstruos dropean un item específico', category: 'Información' },
  { command: 'time', description: 'Muestra la hora actual del juego', category: 'Información' },
  { command: 'jailtime', description: 'Muestra tiempo restante en la cárcel (si aplica)', category: 'Información' },
  { command: 'hominfo', description: 'Muestra información del homúnculo', category: 'Información' },
  { command: 'homstats', description: 'Muestra estadísticas del homúnculo', category: 'Información' },
  { command: 'homtalk', description: 'Permite hablar a través del homúnculo', category: 'Información' },
  { command: 'showexp', description: 'Muestra la experiencia ganada en batalla', category: 'Información' },
  { command: 'showzeny', description: 'Muestra el zeny ganado/perdido', category: 'Información' },
  { command: 'whereis', description: 'Muestra la ubicación de un monstruo', category: 'Información' },
  { command: 'idsearch', description: 'Busca información por ID de item o monstruo', category: 'Información' },
  { command: 'load', description: 'Te envia a la posicion de guardado', category: 'Información' },

  // Feature Commands
  { command: 'refresh', description: 'Actualiza la interfaz del juego', category: 'Características' },
  { command: 'noask', description: 'Bloquea solicitudes de grupo e intercambios', category: 'Características' },
  { command: 'noks', description: 'Activa/desactiva el modo sin KS (Kill Steal)', category: 'Características' },
  { command: 'autoloot', description: 'Activa/desactiva el looteo automático', category: 'Características' },
  { command: 'alootid', description: 'Configura items específicos para autoloot', category: 'Características' },
  { command: 'autoloottype', description: 'Configura tipos de items para autoloot', category: 'Características' },
  { command: 'autotrade', description: 'Inicia el modo de vendedor automático', category: 'Características' },
  { command: 'request', description: 'Envía un mensaje a los gms conectados', category: 'Características' },
  { command: 'go', description: 'Teletransportación rápida a ciudades', category: 'Características' },
  { command: 'breakguild', description: 'Rompe el gremio', category: 'Características' },
  { command: 'channel', description: 'Cambia entre canales del servidor', category: 'Características' },
  { command: 'storage', description: 'Accede al almacén personal', category: 'Características' },
  { command: 'guildstorage', description: 'Accede al almacén del gremio', category: 'Características' },
  { command: 'gstorage', description: 'Alias para guildstorage', category: 'Características' },
  { command: 'langtype', description: 'Cambia el idioma de la interfaz', category: 'Características' },

  // Commands (Custom)
  { command: 'restock', description: 'Reabastece automáticamente items del storage', category: 'Xtreme Pixel' },
  { command: 'restock_list', description: 'Muestra la lista de items para reabastecer', category: 'Xtreme Pixel' },
  { command: 'lastteleport', description: 'Regresa al último punto de teletransporte', category: 'Xtreme Pixel' },
  { command: 'ltp', description: 'Alias para lastteleport', category: 'Xtreme Pixel' },
  { command: 'dance', description: 'Realiza una animación de baile', category: 'Xtreme Pixel' },
  { command: 'afk', description: 'Marca el estado como Ausente', category: 'Xtreme Pixel' },
  { command: 'myinfo', description: 'Muestra información detallada del personaje', category: 'Xtreme Pixel' },
  { command: 'battlestats', description: 'Muestra estadísticas de batalla en tiempo real', category: 'Xtreme Pixel' },
  { command: 'petstats', description: 'Muestra estadísticas de la mascota', category: 'Xtreme Pixel' },
  { command: 'pettalk', description: 'Habilita que la mascota hable automáticamente', category: 'Xtreme Pixel' },
  { command: 'showdamage', description: 'Muestra el daño infligido', category: 'Xtreme Pixel' },
  { command: 'battleinfo', description: 'Muestra información detallada del combate', category: 'Xtreme Pixel' },
  { command: 'hold', description: 'Congela la posición del personaje', category: 'Xtreme Pixel' },
  { command: 'packetfilter', description: 'Filtra paquetes específicos del juego, permite reducir efectos molestos en pantalla', category: 'Xtreme Pixel' },
  { command: 'autorenew', description: 'Renueva automáticamente buffs y efectos', category: 'Xtreme Pixel' },
  { command: 'ar', description: 'Alias para autorenew', category: 'Xtreme Pixel' },
  { command: 'partybuff', description: 'Muestra los buff en party', category: 'Xtreme Pixel' },
  { command: 'spb', description: 'Alias para partybuff', category: 'Xtreme Pixel' },
  { command: 'changegm', description: 'Cambia el maestro de gremio', category: 'Xtreme Pixel' },
  { command: 'cpb', description: 'Cancela los buffs del grupo', category: 'Xtreme Pixel' },
  { command: 'skilltiming', description: 'Muestra temporizadores de habilidades', category: 'Xtreme Pixel' },
  { command: 'hidepet', description: 'Oculta/muestra la mascota', category: 'Xtreme Pixel' },
  { command: 'hidesprite', description: 'Oculta/muestra sprites específicos', category: 'Xtreme Pixel' },
  { command: 'whosell', description: 'Busca quién vende un item específico', category: 'Xtreme Pixel' },
  { command: 'whobuy', description: 'Busca quién compra un item específico', category: 'Xtreme Pixel' },
  { command: 'whoshop', description: 'Muestra información de tiendas abiertas', category: 'Xtreme Pixel' },
  { command: 'autofeed', description: 'Alimenta automáticamente al homúnculo/mascota', category: 'Xtreme Pixel' }
])

// Estadísticas de comandos
const commandsStats = ref({
  totalCommands: commandsData.value.length,
  socialCommands: commandsData.value.filter(cmd => cmd.category === 'Social').length,
  infoCommands: commandsData.value.filter(cmd => cmd.category === 'Información').length,
  featureCommands: commandsData.value.filter(cmd => cmd.category === 'Características').length,
  customCommands: commandsData.value.filter(cmd => cmd.category === 'Xtreme Pixel').length
})

const columns: TableColumn<Command>[] = [
  {
    accessorKey: 'command',
    header: 'Comando',
    cell: ({ row }) => h('div', { 
      class: 'font-mono text-sm text-blue-600 dark:text-blue-400 font-bold' 
    }, `@${row.getValue('command')}`)
  },
  {
    accessorKey: 'description',
    header: 'Descripción',
    cell: ({ row }) => h('div', { 
      class: 'text-gray-700 dark:text-gray-300 text-sm leading-tight' 
    }, row.getValue('description'))
  },
  {
    accessorKey: 'category',
    header: 'Categoría',
    cell: ({ row }) => {
      const category = row.getValue('category') as string
      const colorClass = {
        'Social': 'bg-purple-100 text-purple-800 dark:bg-purple-900 dark:text-purple-300',
        'Información': 'bg-blue-100 text-blue-800 dark:bg-blue-900 dark:text-blue-300',
        'Características': 'bg-green-100 text-green-800 dark:bg-green-900 dark:text-green-300',
        'Xtreme Pixel': 'bg-orange-100 text-orange-800 dark:bg-orange-900 dark:text-orange-300'
      }[category] || 'bg-gray-100 text-gray-800 dark:bg-gray-900 dark:text-gray-300'

      return h('span', { 
        class: `inline-flex items-center px-2.5 py-1 rounded-full text-xs font-bold ${colorClass}`
      }, category)
    }
  }
]

// Filtrar por categoría
const selectedCategory = ref('Todos')
const categories = ['Todos', 'Social', 'Información', 'Características', 'Xtreme Pixel']

const filteredCommands = computed(() => {
  if (selectedCategory.value === 'Todos') {
    return commandsData.value
  }
  return commandsData.value.filter(cmd => cmd.category === selectedCategory.value)
})

// Función auxiliar para contar comandos por categoría
const getCommandsCountByCategory = (category: string) => {
  return commandsData.value.filter(cmd => cmd.category === category).length
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
            Comandos Disponibles
          </h1>
          <p class="text-xl mb-6 text-blue-100">
            Lista completa de comandos para mejorar tu experiencia de juego
          </p>
          <div class="inline-flex items-center gap-4 bg-white/10 backdrop-blur-sm px-6 py-3 rounded-full">
            <UIcon name="i-heroicons-command-line" class="text-yellow-300" />
            <span class="text-sm">{{ commandsStats.totalCommands }} comandos disponibles</span>
            <span class="text-sm">•</span>
            <span class="text-sm">4 categorías</span>
          </div>
        </div>
      </UContainer>
    </div>

    <UContainer class="py-12">
      <!-- Tarjetas de estadísticas -->
      <div class="grid grid-cols-1 md:grid-cols-4 gap-6 mb-12">
        <UCard class="text-center bg-white/80 dark:bg-gray-800/80 backdrop-blur-sm">
          <template #header>
            <h3 class="text-lg font-semibold text-gray-900 dark:text-white">Total Comandos</h3>
          </template>
          <div class="text-3xl font-bold text-purple-600 dark:text-purple-400">
            {{ commandsStats.totalCommands }}
          </div>
          <p class="text-sm text-gray-600 dark:text-gray-400 mt-2">Disponibles</p>
        </UCard>

        <UCard class="text-center bg-white/80 dark:bg-gray-800/80 backdrop-blur-sm">
          <template #header>
            <h3 class="text-lg font-semibold text-gray-900 dark:text-white">Social</h3>
          </template>
          <div class="text-3xl font-bold text-blue-600 dark:text-blue-400">
            {{ commandsStats.socialCommands }}
          </div>
          <p class="text-sm text-gray-600 dark:text-gray-400 mt-2">Interacción</p>
        </UCard>

        <UCard class="text-center bg-white/80 dark:bg-gray-800/80 backdrop-blur-sm">
          <template #header>
            <h3 class="text-lg font-semibold text-gray-900 dark:text-white">Información</h3>
          </template>
          <div class="text-3xl font-bold text-green-600 dark:text-green-400">
            {{ commandsStats.infoCommands }}
          </div>
          <p class="text-sm text-gray-600 dark:text-gray-400 mt-2">Consultas</p>
        </UCard>

        <UCard class="text-center bg-white/80 dark:bg-gray-800/80 backdrop-blur-sm">
          <template #header>
            <h3 class="text-lg font-semibold text-gray-900 dark:text-white">Xtreme Pixel</h3>
          </template>
          <div class="text-3xl font-bold text-orange-600 dark:text-orange-400">
            {{ commandsStats.customCommands }}
          </div>
          <p class="text-sm text-gray-600 dark:text-gray-400 mt-2">Exclusivos</p>
        </UCard>
      </div>

      <!-- Filtros por categoría -->
      <UCard class="mb-6">
        <template #header>
          <div class="flex items-center justify-between">
            <div>
              <h3 class="text-lg font-semibold text-gray-900 dark:text-white mb-1">
                Filtrar por Categoría
              </h3>
              <p class="text-sm text-gray-600 dark:text-gray-400">
                Explora los comandos por tipo de funcionalidad
              </p>
            </div>
            <UBadge color="blue" variant="subtle">
              {{ filteredCommands.length }} mostrados
            </UBadge>
          </div>
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
            <template v-if="category !== 'Todos'">
              <span class="ml-1 bg-white/20 px-1.5 py-0.5 rounded text-xs">
                {{ getCommandsCountByCategory(category) }}
              </span>
            </template>
          </UButton>
        </div>
      </UCard>

      <!-- Tabla de Comandos -->
      <UCard class="mb-12">
        <template #header>
          <div class="flex items-center justify-between">
            <div>
              <h2 class="text-2xl font-bold text-gray-900 dark:text-white flex items-center gap-2">
                <UIcon name="i-heroicons-command-line" class="text-indigo-500" />
                Lista de Comandos Disponibles
              </h2>
              <p class="text-gray-600 dark:text-gray-400 mt-1">
                Comandos disponibles en el servidor con sus descripciones y categorías
              </p>
            </div>
            <UBadge color="indigo" variant="solid" size="lg">
              {{ filteredCommands.length }} Comandos
            </UBadge>
          </div>
        </template>

        <div class="overflow-x-auto">
          <UTable 
            :data="filteredCommands" 
            :columns="columns" 
            class="flex-1 min-w-max"
            :ui="{
              wrapper: 'ring-1 ring-gray-200 dark:ring-gray-800 rounded-lg overflow-hidden',
              thead: 'bg-gradient-to-r from-indigo-50 to-purple-50 dark:from-indigo-900/20 dark:to-purple-900/20',
              tbody: 'divide-y divide-gray-200 dark:divide-gray-800',
              th: 'py-4 px-4 text-left font-bold text-gray-900 dark:text-white whitespace-nowrap',
              td: 'py-3 px-4'
            }"
          />
        </div>

        <!-- Información adicional -->
        <div class="mt-6 grid grid-cols-1 lg:grid-cols-2 gap-4 text-sm">
          <div class="p-4 bg-blue-50 dark:bg-blue-900/20 rounded-lg">
            <h4 class="font-semibold text-blue-800 dark:text-blue-300 mb-2 flex items-center gap-2">
              <UIcon name="i-heroicons-information-circle" class="text-blue-500" />
              Uso de Comandos
            </h4>
            <ul class="text-blue-700 dark:text-blue-400 space-y-1">
              <li>• Todos los comandos empiezan con <code class="bg-blue-100 px-1 rounded">@</code></li>
              <li>• Ejemplo: <code class="bg-blue-100 px-1 rounded">@go</code> para teletransporte</li>
              <li>• Usa <code class="bg-blue-100 px-1 rounded">@help comando</code> para más información</li>
            </ul>
          </div>
          <div class="p-4 bg-green-50 dark:bg-green-900/20 rounded-lg">
            <h4 class="font-semibold text-green-800 dark:text-green-300 mb-2 flex items-center gap-2">
              <UIcon name="i-heroicons-light-bulb" class="text-green-500" />
              Comandos Destacados
            </h4>
            <ul class="text-green-700 dark:text-green-400 space-y-1">
              <li>• <strong>@go</strong>: Teletransporte rápido</li>
              <li>• <strong>@autoloot</strong>: Looteo automático</li>
              <li>• <strong>@myinfo</strong>: Info detallada</li>
              <li>• <strong>@restock</strong>: Reabastecimiento automático</li>
            </ul>
          </div>
        </div>
      </UCard>

      <!-- Sección de Categorías -->
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 mb-12">
        <!-- Comandos Sociales -->
        <UCard>
          <template #header>
            <h3 class="text-xl font-bold text-gray-900 dark:text-white flex items-center gap-2">
              <UIcon name="i-heroicons-users" class="text-purple-500" />
              Comandos Sociales
            </h3>
          </template>
          <div class="space-y-3">
            <div v-for="feature in [
              'Sistema de duelos completo (@duel, @accept, @reject)',
              'Gestión de BG (@vote, @votekick, @leader)',
              'Control de apariencia (@changedress)',
              'Reporte de jugadores AFK (@reportafk)'
            ]" :key="feature" class="flex items-start gap-3">
              <UIcon name="i-heroicons-check-badge" class="text-green-500 flex-shrink-0 mt-0.5" />
              <span class="text-gray-700 dark:text-gray-300 text-sm leading-relaxed">{{ feature }}</span>
            </div>
          </div>
        </UCard>

        <!-- Comandos Xtreme Pixel -->
        <UCard>
          <template #header>
            <h3 class="text-xl font-bold text-gray-900 dark:text-white flex items-center gap-2">
              <UIcon name="i-heroicons-star" class="text-orange-500" />
              Comandos Exclusivos
            </h3>
          </template>
          <div class="space-y-3">
            <div v-for="feature in [
              'Reabastecimiento automático (@restock)',
              'Información detallada (@myinfo, @battlestats)',
              'Control de efectos (@packetfilter, @hidepet)',
              'Automatización (@autorenew, @autofeed)'
            ]" :key="feature" class="flex items-start gap-3">
              <UIcon name="i-heroicons-sparkles" class="text-orange-500 flex-shrink-0 mt-0.5" />
              <span class="text-gray-700 dark:text-gray-300 text-sm leading-relaxed">{{ feature }}</span>
            </div>
          </div>
        </UCard>
      </div>

      <!-- Call to Action -->
      <div class="text-center p-8 bg-gradient-to-r from-indigo-500 to-purple-600 rounded-2xl text-white shadow-xl">
        <h2 class="text-3xl font-bold mb-4">¿Necesitas Más Ayuda?</h2>
        <p class="text-xl mb-6 text-indigo-100">
          Únete a nuestra comunidad para aprender más sobre los comandos y sus usos avanzados
        </p>
        <div class="flex flex-col sm:flex-row gap-4 justify-center">
          <UButton 
            size="xl" 
            color="white" 
            variant="solid"
            class="font-bold text-indigo-600 hover:scale-105 transition-transform"
            href="https://discord.gg/66f3ZfPKBY"
            target="_blank"
          >
            <UIcon name="i-simple-icons-discord" class="w-5 h-5" />
            Comunidad Discord
          </UButton>
        </div>
      </div>
    </UContainer>
  </div>
</template>