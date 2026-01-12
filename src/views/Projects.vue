<template>
  <div class="min-h-screen pt-32 px-6">
    <div class="container mx-auto">
      <div class="mb-16">
        <h1 class="text-5xl font-bold mb-4 uppercase tracking-tighter">
          PROJECTS<span class="text-patronian-gold">.EXE</span>
        </h1>
        <p class="text-gray-500 max-w-xl">
          A selection of high-performance tools, applications, and frameworks built for the next generation of digital infrastructure.
        </p>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
        <div v-for="i in 6" :key="i" 
             class="group relative border border-patronian-white/10 bg-patronian-white/5 p-8 hover:border-patronian-gold/50 transition-all duration-500 overflow-hidden">
          <!-- Decal -->
          <div class="absolute top-0 right-0 p-4 opacity-5 text-4xl font-bold italic">0{{i}}</div>
          
          <div class="h-48 bg-patronian-black/50 border border-patronian-white/10 mb-6 flex items-center justify-center group-hover:bg-patronian-gold/10 transition-colors">
            <div class="w-12 h-1 bg-patronian-gold/20 group-hover:w-24 transition-all"></div>
          </div>
          
          <h3 class="text-xl font-bold mb-2 uppercase tracking-widest">Helix Protocol {{i}}</h3>
          <p class="text-gray-500 text-sm mb-6 leading-relaxed">
            A decentralized communication layer optimized for low-latency streaming and biometric data sync.
          </p>
          
          <div class="flex gap-4">
            <span class="text-[10px] text-patronian-gold border border-patronian-gold px-2 py-0.5 uppercase">Vue 3</span>
            <span class="text-[10px] text-patronian-gold border border-patronian-gold px-2 py-0.5 uppercase">Rust</span>
          </div>
          
          <a href="#" class="absolute bottom-4 right-8 text-patronian-gold opacity-0 group-hover:opacity-100 transition-opacity transform translate-x-4 group-hover:translate-x-0 font-bold">
            VIEW SOURCE →
          </a>
        </div>
      </div>
    </div>
  </div>
</template>
