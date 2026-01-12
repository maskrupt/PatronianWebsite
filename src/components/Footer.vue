<template>
  <footer class="border-t border-patronian-white/10 bg-patronian-black py-12 mt-20">
    <div class="container mx-auto px-6">
      <div class="flex flex-col md:flex-row justify-between items-start gap-12">
        <div class="space-y-4 max-w-sm">
          <div class="text-2xl font-bold tracking-tighter">
            PATRON<span class="text-patronian-gold">IAN</span>
          </div>
          <p class="text-gray-500 text-sm leading-relaxed text-balance">
            Building the decentralized future through high-performance code and engaging community streaming. Join the system.
          </p>
        </div>
        
        <div class="grid grid-cols-2 sm:grid-cols-3 gap-12">
          <div class="space-y-4">
            <h4 class="text-xs uppercase tracking-[0.2em] text-patronian-gold font-bold">Navigation</h4>
            <ul class="space-y-2 text-sm text-gray-400">
              <li><router-link to="/" class="hover:text-white transition-colors">Home</router-link></li>
              <li><router-link to="/about" class="hover:text-white transition-colors">About</router-link></li>
              <li><router-link to="/projects" class="hover:text-white transition-colors">Projects</router-link></li>
            </ul>
          </div>
          <div class="space-y-4">
            <h4 class="text-xs uppercase tracking-[0.2em] text-patronian-gold font-bold">Social</h4>
            <ul class="space-y-2 text-sm text-gray-400">
              <li><a href="#" class="hover:text-white transition-colors">Twitch</a></li>
              <li><a href="#" class="hover:text-white transition-colors">GitHub</a></li>
              <li><a href="#" class="hover:text-white transition-colors">X / Twitter</a></li>
            </ul>
          </div>
          <div class="space-y-4">
            <h4 class="text-xs uppercase tracking-[0.2em] text-patronian-gold font-bold">System</h4>
            <ul class="space-y-2 text-sm text-gray-400">
              <li><a href="#" class="hover:text-white transition-colors">Status</a></li>
              <li><a href="#" class="hover:text-white transition-colors">API</a></li>
            </ul>
          </div>
        </div>
      </div>
      
      <div class="mt-20 pt-8 border-t border-patronian-white/5 flex flex-col sm:flex-row justify-between gap-4 text-[10px] uppercase tracking-widest text-gray-600 font-mono">
        <div>© 2026 PATRONIAN // ALL RIGHTS RESERVED</div>
        <div>DESIGNED FOR THE AUGMENTED FRONTIER</div>
      </div>
    </div>
  </footer>
</template>
