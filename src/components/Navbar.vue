<script setup>
import { ref } from 'vue'
import GameOverlay from './GameOverlay.vue'

const isGameVisible = ref(false)
</script>

<template>
  <nav class="fixed top-0 w-full z-50 border-b border-patronian-white/10 bg-patronian-black/80 backdrop-blur-md">
    <div class="container mx-auto px-6 h-20 flex items-center justify-between">
      <router-link to="/" class="text-2xl font-bold tracking-tighter group">
        PATRON<span class="text-patronian-gold group-hover:text-white transition-colors">IAN</span>
      </router-link>
      
      <div class="hidden md:flex gap-8 text-sm uppercase tracking-widest font-medium">
        <router-link to="/" class="hover:text-patronian-gold transition-colors" active-class="text-patronian-gold">Home</router-link>
        <router-link to="/about" class="hover:text-patronian-gold transition-colors" active-class="text-patronian-gold">About</router-link>
        <router-link to="/projects" class="hover:text-patronian-gold transition-colors" active-class="text-patronian-gold">Projects</router-link>
        <router-link to="/stream" class="hover:text-patronian-gold transition-colors" active-class="text-patronian-gold">Stream</router-link>
        <router-link to="/contact" class="hover:text-patronian-gold transition-colors" active-class="text-patronian-gold">Contact</router-link>
      </div>

      <div class="flex items-center gap-4">
        <div class="hidden sm:block text-[10px] text-gray-500 font-mono text-right">
          STATUS: ONLINE<br/>
          LOC: 127.0.0.1
        </div>
        <div @click="isGameVisible = true" class="w-10 h-10 bg-patronian-gold rounded-full flex items-center justify-center glow-gold cursor-pointer hover:scale-110 transition-transform">
          <div class="w-4 h-4 bg-patronian-black"></div>
        </div>
      </div>
    </div>
  </nav>

  <Teleport to="body">
    <GameOverlay v-if="isGameVisible" @close="isGameVisible = false" />
  </Teleport>
</template>
