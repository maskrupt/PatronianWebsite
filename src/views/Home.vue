<script setup>
import ThreeHero from '../components/ThreeHero.vue'
</script>

<template>
  <div class="min-h-screen bg-patronian-black text-patronian-white overflow-hidden relative">
    <!-- Animated background elements -->
    <div class="absolute top-0 left-0 w-full h-full opacity-20 pointer-events-none">
      <div class="absolute top-10 left-10 w-96 h-96 border border-patronian-gold rounded-full blur-3xl opacity-20 animate-pulse"></div>
      <div class="absolute bottom-10 right-10 w-96 h-96 border border-patronian-accent rounded-full blur-3xl opacity-20 animate-pulse delay-700"></div>
    </div>

    <!-- Main Content -->
    <main class="container mx-auto px-6 pt-32 relative z-10">
      <div class="flex flex-col lg:flex-row items-center gap-12">
        <!-- Hero Text -->
        <div class="flex-1 space-y-8">
          <div class="inline-block px-4 py-1 border border-patronian-gold/30 rounded-full bg-patronian-gold/5 text-patronian-gold text-sm tracking-widest uppercase">
            System Online // Patronian
          </div>
          
          <h1 class="text-6xl lg:text-8xl font-bold leading-tight">
            Leveling Up <br />
            <span class="text-transparent bg-clip-text bg-gradient-to-r from-patronian-gold to-white">
              The Code & The Stream
            </span>
          </h1>
          
          <p class="text-lg text-gray-400 max-w-xl leading-relaxed">
            Software Architect by day, Cyber-Streamer by night. Creating high-performance digital experiences and sharing the journey in real-time.
          </p>

          <div class="flex flex-wrap gap-4">
            <router-link to="/projects" class="px-8 py-3 bg-patronian-gold text-patronian-black font-bold uppercase tracking-wider hover:bg-white transition-colors duration-300 transform hover:scale-105">
              View Projects
            </router-link>
            <router-link to="/stream" class="px-8 py-3 border border-patronian-white/30 hover:border-patronian-gold transition-colors duration-300 font-bold uppercase tracking-wider">
              Enter Stream
            </router-link>
          </div>
        </div>

        <!-- Hero Decorative Asset (Simulating the Gold Prosthetic Style) -->
        <div class="flex-1 relative">
          <div class="w-72 h-72 md:w-96 md:h-96 relative mx-auto group">
             <!-- 3D Scene Layer -->
             <div class="absolute inset-0 z-0 pointer-events-none opacity-60">
                <ThreeHero />
             </div>

             <!-- Animated boundary -->
             <div class="absolute inset-0 border-2 border-patronian-gold/20 rotate-45 animate-spin-slow group-hover:border-patronian-gold/50 transition-colors z-10"></div>
             <div class="absolute inset-0 border-2 border-patronian-gold/10 -rotate-12 z-10"></div>
             
             <!-- Anime Portrait Container -->
             <div class="absolute inset-4 bg-gradient-to-br from-patronian-white/10 to-transparent backdrop-blur-sm border border-patronian-white/20 flex items-center justify-center overflow-hidden grayscale hover:grayscale-0 transition-all duration-700 z-20">
               <div class="w-full h-full bg-patronian-black/40 relative flex items-center justify-center">
                 <!-- 
                    Anime Portrait 
                 -->
                 <img src="../assets/home.jpg" 
                      alt="Patronian Anime Portrait" 
                      class="w-full h-full object-cover opacity-80 group-hover:opacity-100 transition-opacity">
                 
                 <!-- Scanning effect -->
                 <div class="absolute inset-0 bg-gradient-to-b from-transparent via-patronian-gold/10 to-transparent h-1/4 w-full animate-scan pointer-events-none"></div>
               </div>
             </div>
             
             <!-- Gold accents mirroring the prosthetic -->
             <div class="absolute -right-4 top-1/2 w-8 h-32 bg-patronian-gold glow-gold shadow-[0_0_30px_#d4af37]"></div>
             <div class="absolute -left-4 bottom-1/4 w-8 h-16 bg-patronian-white/20 border-r border-patronian-gold/50"></div>
          </div>
        </div>
      </div>

      <!-- Stats / Features -->
      <div class="grid grid-cols-1 md:grid-cols-3 gap-8 mt-24 border-t border-patronian-white/10 pt-12">
        <div class="space-y-2">
          <div class="text-patronian-gold text-3xl font-bold">12+</div>
          <div class="text-sm uppercase tracking-widest text-gray-500">Years XP</div>
        </div>
        <div class="space-y-2">
          <div class="text-white text-3xl font-bold">50K+</div>
          <div class="text-sm uppercase tracking-widest text-gray-500">Lines Composed</div>
        </div>
        <div class="space-y-2">
          <div class="text-patronian-accent text-3xl font-bold">3.5GHz</div>
          <div class="text-sm uppercase tracking-widest text-gray-500">Mental Clock</div>
        </div>
      </div>
    </main>
  </div>
</template>

<style scoped>
.animate-spin-slow {
  animation: spin 8s linear infinite;
}

@keyframes spin {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

@keyframes glow {
  0%, 100% { opacity: 0.5; height: 1px; }
  50% { opacity: 1; height: 4px; box-shadow: 0 0 15px #d4af37; }
}

@keyframes scan {
  from { transform: translateY(-100%); }
  to { transform: translateY(400%); }
}

.animate-glow {
  animation: glow 3s ease-in-out infinite;
}

.animate-scan {
  animation: scan 4s linear infinite;
}
</style>
