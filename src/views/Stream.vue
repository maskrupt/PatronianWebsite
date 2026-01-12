<template>
  <div class="min-h-screen pt-32 px-6">
    <div class="container mx-auto">
      <div class="flex flex-col lg:flex-row gap-12">
        <div class="lg:w-2/3 space-y-8">
          <div class="relative aspect-video bg-patronian-black border border-patronian-gold/30 glow-gold overflow-hidden">
            <!-- Kick Stream Embed -->
            <iframe 
              src="https://player.kick.com/patronian" 
              class="absolute inset-0 w-full h-full border-0"
              frameborder="0" 
              scrolling="no" 
              allowfullscreen="true">
            </iframe>
            
            <!-- UI Overlay (Decorative only when not hovered/to keep style) -->
            <div class="absolute top-4 left-4 flex gap-2 pointer-events-none">
              <span class="px-2 py-1 bg-red-600 text-[10px] font-bold uppercase animate-pulse">LIVE FEED</span>
              <span class="px-2 py-1 bg-patronian-black/80 text-[10px] text-gray-400 font-bold uppercase">4K / 60FPS</span>
            </div>
          </div>
          
          <div class="p-8 border border-patronian-white/10 bg-patronian-white/5 space-y-4">
            <h2 class="text-2xl font-bold uppercase tracking-widest border-l-2 border-patronian-gold pl-4">Now Building: Neural Interface for Vue</h2>
            <p class="text-gray-400 leading-relaxed">
              Today we are deep-diving into the reactive system of Vue and how to bridge it with hardware-accelerated WebGL components. Strap in.
            </p>
          </div>
        </div>

        <div class="lg:w-1/3 space-y-8">
           <div class="p-6 border border-patronian-white/10 bg-patronian-white/5">
             <h3 class="text-sm font-bold uppercase tracking-[0.3em] mb-6 text-patronian-gold">Upcoming Transmission</h3>
             <div class="space-y-6">
               <div v-for="d in ['MON', 'WED', 'FRI']" :key="d" class="flex items-center justify-between border-b border-patronian-white/5 pb-4">
                 <div>
                   <div class="text-lg font-bold">{{ d }}</div>
                   <div class="text-xs text-gray-500 uppercase">System Maintenance</div>
                 </div>
                 <div class="text-right">
                   <div class="text-sm font-mono uppercase">20:00 UTC</div>
                   <div class="text-[10px] text-patronian-gold uppercase">Dev + Chill</div>
                 </div>
               </div>
             </div>
           </div>

           <div class="p-6 border border-patronian-gold/20 bg-patronian-gold/5 flex items-center justify-between group cursor-pointer hover:bg-patronian-gold/10 transition-colors">
             <div>
               <div class="text-sm font-bold uppercase tracking-widest">Support the System</div>
               <div class="text-xs text-gray-500 uppercase">Access exclusive terminal logs</div>
             </div>
             <div class="text-2xl group-hover:translate-x-1 transition-transform">→</div>
           </div>
        </div>
      </div>
    </div>
  </div>
</template>
