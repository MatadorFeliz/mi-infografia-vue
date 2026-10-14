<script setup>
defineProps({
  title: String,
  subtitle: String,
  icon: String,
  badge: String
})
</script>

<template>
  <div class="bg-slate-900 border border-slate-800 rounded-2xl p-6 shadow-xl hover:border-cyan-500/50 transition-all duration-300 flex flex-col justify-between">
    <div>
      <div class="flex items-center justify-between mb-4">
        <span class="text-3xl">{{ icon }}</span>
        <span class="text-xs font-semibold px-3 py-1 bg-cyan-950 text-cyan-400 rounded-full border border-cyan-800/50">
          {{ badge }}
        </span>
      </div>
      
      <h3 class="text-xl font-bold text-white mb-1 tracking-tight">{{ title }}</h3>
      <h4 class="text-sm font-medium text-cyan-400 mb-4">{{ subtitle }}</h4>
      
      <div class="text-slate-300 text-sm leading-relaxed space-y-2">
        <slot></slot>
      </div>
    </div>
    
    <div class="mt-6 pt-4 border-t border-slate-800/80 flex items-center justify-between text-xs text-slate-500 font-mono">
      <span>MODULO_INFOGRAFIA</span>
      <span>VUE 3 // TAILWIND</span>
    </div>
  </div>
</template>