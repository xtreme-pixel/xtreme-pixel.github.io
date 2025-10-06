<script setup lang="ts">

useHead({
  title: 'Descarga',
  meta: [
    { name: 'description', content: 'Cliente de Xtreme Pixel' }
  ]
})

// Datos de enlaces de descarga
const downloadLinks = ref([
  {
    name: 'MEGA',
    icon: 'i-simple-icons-mega',
    color: 'red',
    description: 'Descarga rápida y confiable',
    features: ['Alta velocidad', 'Resumen de descarga', 'Encriptación'],
    url: 'https://mega.nz/file/yJthxQhC#koOkOC77aAuFL30mmfhFM8_ICtiuUG1yjIGHiOMj4cE',
    target: '_blank',
    status: 'Disponible'
  },
  {
    name: 'MediaFire',
    icon: 'i-simple-icons-mediafire',
    color: 'blue',
    description: 'Servicio de descarga directa',
    features: ['Descarga directa', 'Sin esperas', 'Fácil acceso'],
    url: 'https://www.mediafire.com/file/mvhe8xp1o1ca7yb/XtremePixel.rar/file',
    target: '_blank',
    status: 'Disponible'
  },
  {
    name: 'Google Drive',
    icon: 'i-simple-icons-googledrive',
    color: 'green',
    description: 'Almacenamiento en la nube',
    features: ['Acceso inmediato', 'Integración con Google', 'Descarga segura'],
    url: 'https://drive.google.com/file/d/1n_bNQknxyt5vLG-H5YkUMeikYmMShdPS/view?usp=sharing',
    target: '_blank',
    status: 'Disponible'
  }
])

// Requisitos del sistema
const systemRequirements = ref({
  minimum: {
    os: 'Windows 10',
    processor: 'Celeron o Athlon (o mejor)',
    memory: '2GB de RAM',
    graphics: 'Cualquiera con aceleración de graficos 3D y 64MB RAM',
    directx: 'Versión 8.1',
    storage: '8 GB de espacio disponible',
    sound: 'DirectSound (o compatibilidad con efectos de sonido 3D)',
    notes: 'Puede haber problemas de renderizado con graficas Nvidia'
  },
  recommended: {
    os: 'Windows 10 o Windows 11',
    processor: 'Intel i3 o AMD Ryzen 3',
    memory: '4 GB de RAM',
    graphics: 'Nvidia GeForce 8000 or better',
    directx: 'Versión 8.1',
    network: 'Conexión de banda ancha a Internet',
    storage: '10 GB de espacio disponible',
    sound: 'DirectSound (o compatibilidad con efectos de sonido 3D)'
  }
})

// Pasos de instalación
const installationSteps = ref([
  'Descarga el cliente completo desde cualquiera de los enlaces',
  'Descomprime el archivo ZIP en la ubicación deseada',
  'Configura el cliente con Setup.exe o dinput.ini',
  'Ejecuta el archivo "XtremePixel.exe" como administrador',
  'Crea tu cuenta: nombre_M o nombre_F',
  '¡Listo para jugar!'
])

// Estadísticas de descarga
const downloadStats = ref({
  totalDownloads: '15,842',
  lastUpdate: '5 Octubre 2025',
  fileSize: '5.0 GB',
  version: 'v1.0.0'
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
            Descargas
          </h1>
          <p class="text-xl mb-6 text-blue-100">
            Cliente completo • Parches • Actualizaciones
          </p>
          <div class="inline-flex items-center gap-4 bg-white/10 backdrop-blur-sm px-6 py-3 rounded-full">
            <UIcon name="i-heroicons-information-circle" class="text-yellow-300" />
            <span class="text-sm">Versión actual: {{ downloadStats.version }}</span>
            <span class="text-sm">•</span>
            <span class="text-sm">Tamaño: {{ downloadStats.fileSize }}</span>
          </div>
        </div>
      </UContainer>
    </div>

    <UContainer class="py-12">
      <!-- Tarjetas de estadísticas -->
      <div class="grid grid-cols-1 md:grid-cols-4 gap-6 mb-12">
        <UCard class="text-center bg-white/80 dark:bg-gray-800/80 backdrop-blur-sm">
          <template #header>
            <h3 class="text-lg font-semibold text-gray-900 dark:text-white">Tipo de Instalador</h3>
          </template>
          <div class="text-3xl font-bold text-green-600 dark:text-green-400">Zip</div>
          <p class="text-sm text-gray-600 dark:text-gray-400 mt-2">Requiere Winrar o similar</p>
        </UCard>

        <UCard class="text-center bg-white/80 dark:bg-gray-800/80 backdrop-blur-sm">
          <template #header>
            <h3 class="text-lg font-semibold text-gray-900 dark:text-white">Última Actualización</h3>
          </template>
          <div class="text-xl font-bold text-blue-600 dark:text-blue-400">
            {{ downloadStats.lastUpdate }}
          </div>
          <p class="text-sm text-gray-600 dark:text-gray-400 mt-2">Cliente actualizado</p>
        </UCard>

        <UCard class="text-center bg-white/80 dark:bg-gray-800/80 backdrop-blur-sm">
          <template #header>
            <h3 class="text-lg font-semibold text-gray-900 dark:text-white">Tamaño del Cliente</h3>
          </template>
          <div class="text-2xl font-bold text-purple-600 dark:text-purple-400">
            {{ downloadStats.fileSize }}
          </div>
          <p class="text-sm text-gray-600 dark:text-gray-400 mt-2">Comprimido</p>
        </UCard>

        <UCard class="text-center bg-white/80 dark:bg-gray-800/80 backdrop-blur-sm">
          <template #header>
            <h3 class="text-lg font-semibold text-gray-900 dark:text-white">Versión</h3>
          </template>
          <div class="text-2xl font-bold text-orange-600 dark:text-orange-400">
            {{ downloadStats.version }}
          </div>
          <p class="text-sm text-gray-600 dark:text-gray-400 mt-2">Estable</p>
        </UCard>
      </div>

      <!-- Enlaces de Descarga -->
      <UCard class="mb-12">
        <template #header>
          <div class="flex items-center justify-between">
            <div>
              <h2 class="text-2xl font-bold text-gray-900 dark:text-white flex items-center gap-2">
                <UIcon name="i-heroicons-arrow-down-tray" class="text-green-500" />
                Descargar Cliente
              </h2>
              <p class="text-gray-600 dark:text-gray-400 mt-1">
                Elige tu plataforma de descarga preferida
              </p>
            </div>
            <UBadge color="green" variant="solid" size="lg">
              Todos Disponibles
            </UBadge>
          </div>
        </template>

        <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
          <div 
            v-for="(link, index) in downloadLinks" 
            :key="index"
            class="group relative bg-gradient-to-br from-white to-gray-50 dark:from-gray-800 dark:to-gray-700 border-2 border-gray-200 dark:border-gray-600 rounded-xl p-6 hover:shadow-xl transition-all duration-300 hover:scale-105"
            :class="{
              'hover:border-red-300 dark:hover:border-red-600': link.color === 'red',
              'hover:border-blue-300 dark:hover:border-blue-600': link.color === 'blue',
              'hover:border-green-300 dark:hover:border-green-600': link.color === 'green'
            }"
          >
            <!-- Header de la tarjeta -->
            <div class="flex items-center justify-between mb-4">
              <div class="flex items-center gap-3">
                <UIcon 
                  :name="link.icon" 
                  class="text-2xl"
                  :class="{
                    'text-red-500': link.color === 'red',
                    'text-blue-500': link.color === 'blue',
                    'text-green-500': link.color === 'green'
                  }"
                />
                <h3 class="text-xl font-bold text-gray-900 dark:text-white">
                  {{ link.name }}
                </h3>
              </div>
              <UBadge 
                :color="link.color as any" 
                variant="subtle"
                class="capitalize"
              >
                {{ link.status }}
              </UBadge>
            </div>

            <!-- Descripción -->
            <p class="text-gray-600 dark:text-gray-400 mb-4">
              {{ link.description }}
            </p>

            <!-- Características -->
            <div class="space-y-2 mb-6">
              <div 
                v-for="(feature, featureIndex) in link.features" 
                :key="featureIndex"
                class="flex items-center gap-2 text-sm"
              >
                <UIcon name="i-heroicons-check-circle" class="text-green-500 flex-shrink-0" />
                <span class="text-gray-700 dark:text-gray-300">{{ feature }}</span>
              </div>
            </div>

            <!-- Botón de descarga -->
            <UButton
              :color="link.color as any"
              variant="solid"
              size="lg"
              :block="true"
              class="font-bold"
              :ui="{ rounded: 'rounded-lg' }"
              :href="link.url"
              :target="link.target"
            >
              <UIcon name="i-heroicons-arrow-down-tray" class="w-5 h-5" />
              Descargar desde {{ link.name }}
            </UButton>
          </div>
        </div>
      </UCard>

      <!-- Grid de Requisitos e Instalación -->
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 mb-12">
        <!-- Requisitos del Sistema -->
        <UCard>
          <template #header>
            <h3 class="text-2xl font-bold text-gray-900 dark:text-white flex items-center gap-2">
              <UIcon name="i-heroicons-computer-desktop" class="text-blue-500" />
              Requisitos del Sistema
            </h3>
          </template>

          <div class="space-y-6">
            <!-- Mínimos -->
            <div>
              <h4 class="text-lg font-semibold text-gray-900 dark:text-white mb-3 flex items-center gap-2">
                <UIcon name="i-heroicons-exclamation-triangle" class="text-orange-500" />
                Mínimos
              </h4>
              <div class="space-y-2 text-sm">
                <div class="flex justify-between py-2 border-b border-gray-200 dark:border-gray-700">
                  <span class="text-gray-600 dark:text-gray-400 font-medium">SO:</span>
                  <span class="text-gray-900 dark:text-white text-right">{{ systemRequirements.minimum.os }}</span>
                </div>
                <div class="flex justify-between py-2 border-b border-gray-200 dark:border-gray-700">
                  <span class="text-gray-600 dark:text-gray-400 font-medium">Procesador:</span>
                  <span class="text-gray-900 dark:text-white text-right">{{ systemRequirements.minimum.processor }}</span>
                </div>
                <div class="flex justify-between py-2 border-b border-gray-200 dark:border-gray-700">
                  <span class="text-gray-600 dark:text-gray-400 font-medium">Memoria:</span>
                  <span class="text-gray-900 dark:text-white text-right">{{ systemRequirements.minimum.memory }}</span>
                </div>
                <div class="flex justify-between py-2 border-b border-gray-200 dark:border-gray-700">
                  <span class="text-gray-600 dark:text-gray-400 font-medium">Gráficos:</span>
                  <span class="text-gray-900 dark:text-white text-right">{{ systemRequirements.minimum.graphics }}</span>
                </div>
                <div class="flex justify-between py-2 border-b border-gray-200 dark:border-gray-700">
                  <span class="text-gray-600 dark:text-gray-400 font-medium">DirectX:</span>
                  <span class="text-gray-900 dark:text-white text-right">{{ systemRequirements.minimum.directx }}</span>
                </div>
                <div class="flex justify-between py-2 border-b border-gray-200 dark:border-gray-700">
                  <span class="text-gray-600 dark:text-gray-400 font-medium">Almacenamiento:</span>
                  <span class="text-gray-900 dark:text-white text-right">{{ systemRequirements.minimum.storage }}</span>
                </div>
                <div class="py-2 text-orange-600 dark:text-orange-400 text-xs">
                  {{ systemRequirements.minimum.notes }}
                </div>
              </div>
            </div>

            <!-- Recomendados -->
            <div>
              <h4 class="text-lg font-semibold text-gray-900 dark:text-white mb-3 flex items-center gap-2">
                <UIcon name="i-heroicons-check-badge" class="text-green-500" />
                Recomendados
              </h4>
              <div class="space-y-2 text-sm">
                <div class="flex justify-between py-2 border-b border-gray-200 dark:border-gray-700">
                  <span class="text-gray-600 dark:text-gray-400 font-medium">SO:</span>
                  <span class="text-gray-900 dark:text-white text-right">{{ systemRequirements.recommended.os }}</span>
                </div>
                <div class="flex justify-between py-2 border-b border-gray-200 dark:border-gray-700">
                  <span class="text-gray-600 dark:text-gray-400 font-medium">Procesador:</span>
                  <span class="text-gray-900 dark:text-white text-right">{{ systemRequirements.recommended.processor }}</span>
                </div>
                <div class="flex justify-between py-2 border-b border-gray-200 dark:border-gray-700">
                  <span class="text-gray-600 dark:text-gray-400 font-medium">Memoria:</span>
                  <span class="text-gray-900 dark:text-white text-right">{{ systemRequirements.recommended.memory }}</span>
                </div>
                <div class="flex justify-between py-2 border-b border-gray-200 dark:border-gray-700">
                  <span class="text-gray-600 dark:text-gray-400 font-medium">Gráficos:</span>
                  <span class="text-gray-900 dark:text-white text-right">{{ systemRequirements.recommended.graphics }}</span>
                </div>
                <div class="flex justify-between py-2 border-b border-gray-200 dark:border-gray-700">
                  <span class="text-gray-600 dark:text-gray-400 font-medium">Red:</span>
                  <span class="text-gray-900 dark:text-white text-right">{{ systemRequirements.recommended.network }}</span>
                </div>
              </div>
            </div>
          </div>
        </UCard>

        <!-- Guía de Instalación -->
        <UCard>
          <template #header>
            <h3 class="text-2xl font-bold text-gray-900 dark:text-white flex items-center gap-2">
              <UIcon name="i-heroicons-wrench-screwdriver" class="text-purple-500" />
              Guía de Instalación
            </h3>
          </template>

          <div class="space-y-4">
            <div 
              v-for="(step, index) in installationSteps" 
              :key="index"
              class="flex items-start gap-4 p-4 bg-gradient-to-r from-gray-50 to-blue-50 dark:from-gray-800 dark:to-blue-900/20 rounded-lg"
            >
              <div class="flex-shrink-0 w-8 h-8 bg-blue-500 text-white rounded-full flex items-center justify-center font-bold text-sm">
                {{ index + 1 }}
              </div>
              <p class="text-gray-700 dark:text-gray-300 leading-relaxed">
                {{ step }}
              </p>
            </div>
          </div>

          <!-- Notas adicionales -->
          <div class="mt-6 p-4 bg-yellow-50 dark:bg-yellow-900/20 border border-yellow-200 dark:border-yellow-800 rounded-lg">
            <div class="flex items-start gap-3">
              <UIcon name="i-heroicons-exclamation-triangle" class="text-yellow-500 flex-shrink-0 mt-0.5" />
              <div>
                <h4 class="font-semibold text-yellow-800 dark:text-yellow-300 mb-1">Notas Importantes</h4>
                <ul class="text-sm text-yellow-700 dark:text-yellow-400 space-y-1">
                  <li>• Ejecuta siempre el juego como administrador</li>
                  <li>• Añade a carpeta del servidor a la white list del antivirus</li>
                  <li>• Asegúrate de tener Windows actualizado</li>
                </ul>
              </div>
            </div>
          </div>
        </UCard>
      </div>

      <!-- Call to Action -->
      <div class="text-center p-8 bg-gradient-to-r from-green-500 to-emerald-600 rounded-2xl text-white shadow-xl">
        <h2 class="text-3xl font-bold mb-4">¿Necesitas Ayuda?</h2>
        <p class="text-xl mb-6 text-green-100">
          Únete a nuestro Discord para soporte técnico y ayuda con la instalación
        </p>
        <div class="flex flex-col sm:flex-row gap-4 justify-center">
          <UButton 
            size="xl" 
            color="gray" 
            variant="outline"
            class="font-bold border-white text-white hover:bg-white hover:text-green-600 transition-all"
            href="https://discord.gg/66f3ZfPKBY"
            target="_blank"
          >
            <UIcon name="i-simple-icons-discord" class="w-5 h-5" />
            Soporte en Discord
          </UButton>
        </div>
      </div>
    </UContainer>
  </div>
</template>