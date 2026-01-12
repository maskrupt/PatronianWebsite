<template>
  <div class="min-h-screen pt-32 px-6">
    <div class="container mx-auto max-w-4xl">
      <div class="grid md:grid-cols-2 gap-16">
        <div>
          <h1 class="text-5xl font-bold mb-8 uppercase tracking-tighter">CONTACT<br/><span class="text-patronian-gold">CONNECTION</span></h1>
          <p class="text-gray-400 mb-12 leading-relaxed">
            Need high-performance architecture? Partnership for the stream? Or just want to sync datasets? Send a packet.
          </p>

          <div class="space-y-8">
            <div v-for="link in [ {n:'Email', v:'admin@patronian.io'}, {n:'Matrix', v:'@patronian:matrix.org'}, {n:'Location', v:'Digital Frontier'} ]" 
                 :key="link.n" class="group">
              <div class="text-[10px] uppercase tracking-[0.3em] text-patronian-gold mb-1 font-bold">{{ link.n }}</div>
              <div class="text-lg font-mono text-patronian-white group-hover:text-white transition-colors">{{ link.v }}</div>
            </div>
          </div>
        </div>

        <div class="p-8 border border-patronian-white/10 bg-patronian-white/5 relative">
          <!-- Corner Accents -->
          <div class="absolute top-0 left-0 w-4 h-4 border-t border-l border-patronian-gold"></div>
          <div class="absolute bottom-0 right-0 w-4 h-4 border-b border-r border-patronian-gold"></div>

          <form @submit.prevent class="space-y-6">
            <div class="space-y-2">
              <label class="text-[10px] uppercase tracking-widest text-gray-500 font-bold">Protocol Name</label>
              <input type="text" placeholder="John Doe" class="w-full bg-patronian-black border border-patronian-white/10 p-4 focus:border-patronian-gold outline-none transition-colors font-mono">
            </div>
            <div class="space-y-2">
              <label class="text-[10px] uppercase tracking-widest text-gray-500 font-bold">Return Address</label>
              <input type="email" placeholder="john@example.com" class="w-full bg-patronian-black border border-patronian-white/10 p-4 focus:border-patronian-gold outline-none transition-colors font-mono">
            </div>
            <div class="space-y-2">
              <label class="text-[10px] uppercase tracking-widest text-gray-500 font-bold">Encoded Message</label>
              <textarea rows="4" placeholder="Your packet payload..." class="w-full bg-patronian-black border border-patronian-white/10 p-4 focus:border-patronian-gold outline-none transition-colors font-mono"></textarea>
            </div>
            <button class="w-full py-4 bg-patronian-gold text-patronian-black font-bold uppercase tracking-widest hover:bg-white transition-all transform hover:scale-[1.02]">
              Send Transmission
            </button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>
