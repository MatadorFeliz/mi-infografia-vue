<script setup>
import { ref } from 'vue'
import InfographicCard from './InfographicCard.vue'

// Control de vista: 'infographic' (modo scroll) o 'slides' (modo diapositiva)
const viewMode = ref('infographic')
const currentSlide = ref(0)

// Contenido de la presentación sobre tecnología[cite: 2]
const slidesData = [
  {
    title: "Paradigmas de Ejecución",
    subtitle: "Compilación vs Interpretación & JIT",
    icon: "⚡",
    badge: "Arquitectura",
    content: "Los lenguajes modernos hibridan enfoques. Motores como V8 (JavaScript) o PyPy usan compilación Just-In-Time (JIT) para traducir bytecode a código máquina en tiempo de ejecución, optimizando el rendimiento."
  },
  {
    title: "Gestión de Memoria",
    subtitle: "Garbage Collection vs Ownership",
    icon: "🧠",
    badge: "Sistemas",
    content: "Lenguajes administrados automatizan la recolección de basura, mientras que modelos como Rust implementan reglas de propiedad ('ownership') verificadas en tiempo de compilación sin costo en ejecución."
  },
  {
    title: "Concurrencia y Paralelismo",
    subtitle: "Event Loop y Hilos Livianos",
    icon: "⚙️",
    badge: "Procesamiento",
    content: "La gestión de entrada/salida eficiente en sistemas modernos utiliza modelos asíncronos y 'goroutines' o hilos verdes para manejar miles de peticiones simultáneas sin bloquear el sistema operativo."
  },
  {
    title: "Sistemas de Tipado",
    subtitle: "Estático, Dinámico y Gradual",
    icon: "🛡️",
    badge: "Seguridad de Código",
    content: "El tipado estático avanzado y gradual (como TypeScript) permite detectar errores en tiempo de compilación/desarrollo, aumentando la mantenibilidad en proyectos de gran escala."
  }
]

const nextSlide = () => {
  if (currentSlide.value < slidesData.length - 1) currentSlide.value++
}

const prevSlide = () => {
  if (currentSlide.value > 0) currentSlide.value--
}
</script>

<template>
  <div class="min-h-screen bg-slate-950 text-slate-100 p-6 md:p-12 font-sans">
    
    <!-- Encabezado -->
    <header class="max-w-5xl mx-auto mb-10 text-center">
      <span class="px-3 py-1 bg-cyan-500/10 border border-cyan-500/30 rounded-full text-cyan-400 text-xs font-mono uppercase tracking-wider">
        Infografía & Presentación Técnica
      </span>
      <h1 class="text-3xl md:text-5xl font-extrabold text-white mt-4 mb-3">
        Arquitectura de Lenguajes Modernos
      </h1>
      <p class="text-slate-400 text-sm md:text-base max-w-2xl mx-auto">
        Demostración del sistema construido en Vue 3 y Tailwind CSS.
      </p>

      <!-- Botones para alternar modo infografía / diapositiva[cite: 2] -->
      <div class="flex justify-center gap-3 mt-6">
        <button 
          @click="viewMode = 'infographic'"
          :class="viewMode === 'infographic' ? 'bg-cyan-600 text-white' : 'bg-slate-900 text-slate-400 hover:bg-slate-800'"
          class="px-4 py-2 rounded-lg text-xs font-semibold border border-slate-800 transition-all">
          Modo Infografía (Scroll)
        </button>
        <button 
          @click="viewMode = 'slides'"
          :class="viewMode === 'slides' ? 'bg-cyan-600 text-white' : 'bg-slate-900 text-slate-400 hover:bg-slate-800'"
          class="px-4 py-2 rounded-lg text-xs font-semibold border border-slate-800 transition-all">
          Modo Diapositivas (Deck)
        </button>
      </div>
    </header>

    <!-- Contenido Adaptativo -->
    <main class="max-w-5xl mx-auto">
      <!-- MODO 1: INFOGRAFÍA -->
      <div v-if="viewMode === 'infographic'" class="grid grid-cols-1 md:grid-cols-2 gap-6">
        <InfographicCard 
          v-for="(item, index) in slidesData" 
          :key="index"
          :title="item.title"
          :subtitle="item.subtitle"
          :icon="item.icon"
          :badge="item.badge">
          <p>{{ item.content }}</p>
        </InfographicCard>
      </div>

      <!-- MODO 2: DIAPOSITIVAS -->
      <div v-else class="max-w-2xl mx-auto">
        <InfographicCard 
          :title="slidesData[currentSlide].title"
          :subtitle="slidesData[currentSlide].subtitle"
          :icon="slidesData[currentSlide].icon"
          :badge="slidesData[currentSlide].badge">
          <p class="text-base">{{ slidesData[currentSlide].content }}</p>
        </InfographicCard>

        <!-- Controles de navegación -->
        <div class="flex items-center justify-between mt-6">
          <button 
            @click="prevSlide" 
            :disabled="currentSlide === 0"
            class="px-4 py-2 bg-slate-900 hover:bg-slate-800 disabled:opacity-30 disabled:cursor-not-allowed text-xs font-semibold rounded-lg border border-slate-800">
            Anterior
          </button>
          <span class="text-xs font-mono text-slate-400">
            {{ currentSlide + 1 }} / {{ slidesData.length }}
          </span>
          <button 
            @click="nextSlide" 
            :disabled="currentSlide === slidesData.length - 1"
            class="px-4 py-2 bg-slate-900 hover:bg-slate-800 disabled:opacity-30 disabled:cursor-not-allowed text-xs font-semibold rounded-lg border border-slate-800">
            Siguiente
          </button>
        </div>
      </div>
    </main>

  </div>
</template>