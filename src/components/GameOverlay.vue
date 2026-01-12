<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import * as THREE from 'three';

const emit = defineEmits(['close']);

const containerRef = ref(null);
const score = ref(0);
const highScore = ref(0);
const isNewRecord = ref(false);
const gameOver = ref(false);
const gameStarted = ref(false);

let scene, camera, renderer, blocks = [];
let animationId;
const BLOCK_SIZE = 1.2;
const SPAWN_Z = -25;
const KILL_Z = 12;
const BASE_SPEED = 0.12;
let frameCount = 0;
const raycaster = new THREE.Raycaster();
const mouse = new THREE.Vector2();

const initGame = () => {
  if (scene) {
    blocks.forEach(b => scene.remove(b.mesh));
  }
  blocks = [];
  score.value = 0;
  isNewRecord.value = false;
  gameOver.value = false;
  gameStarted.value = false;
  frameCount = 0;
};

const createBlock = () => {
  const x = (Math.random() - 0.5) * 12; // Slightly wider spawn area
  
  const geometry = new THREE.BoxGeometry(BLOCK_SIZE, BLOCK_SIZE, BLOCK_SIZE);
  const material = new THREE.MeshPhongMaterial({ 
    color: 0xd4af37, 
    emissive: 0xd4af37,
    emissiveIntensity: 0.3,
    transparent: true,
    opacity: 0.9,
    shininess: 100
  });

  const mesh = new THREE.Mesh(geometry, material);
  mesh.position.set(x, BLOCK_SIZE/2, SPAWN_Z);
  
  // Add wireframe overlay for tech look
  const wireGeo = new THREE.EdgesGeometry(geometry);
  const wireMat = new THREE.LineBasicMaterial({ color: 0xffffff, linewidth: 2 });
  const wireframe = new THREE.LineSegments(wireGeo, wireMat);
  mesh.add(wireframe);

  scene.add(mesh);
  blocks.push({ mesh, passed: false });
};

const setupScene = () => {
  scene = new THREE.Scene();
  scene.background = new THREE.Color(0x0a0a0a);
  scene.fog = new THREE.Fog(0x0a0a0a, 10, 30);

  camera = new THREE.PerspectiveCamera(60, 400 / 500, 0.1, 1000);
  camera.position.set(0, 8, 15);
  camera.lookAt(0, 0, -5);

  renderer = new THREE.WebGLRenderer({ antialias: true });
  renderer.setSize(400, 500);
  containerRef.value.appendChild(renderer.domElement);

  // Lights
  const ambientLight = new THREE.AmbientLight(0xffffff, 0.4);
  scene.add(ambientLight);
  const pointLight = new THREE.PointLight(0xd4af37, 2, 100);
  pointLight.position.set(0, 10, 0);
  scene.add(pointLight);

  // Ground Grid
  const gridHelper = new THREE.GridHelper(100, 50, 0xd4af37, 0x1a1a1a);
  scene.add(gridHelper);

  initGame();
};

const handleClick = (event) => {
  if (gameOver.value) {
    initGame();
    return;
  }
  if (!gameStarted.value) {
    gameStarted.value = true;
    return;
  }

  // Use offsetX/Y for more reliable local coordinates
  // Normalize to -1 to +1
  const rect = containerRef.value.getBoundingClientRect();
  mouse.x = ((event.clientX - rect.left) / rect.width) * 2 - 1;
  mouse.y = -((event.clientY - rect.top) / rect.height) * 2 + 1;

  raycaster.setFromCamera(mouse, camera);
  
  // Use recursive: true to hit meshes or their child wireframes
  const intersects = raycaster.intersectObjects(scene.children, true);

  if (intersects.length > 0) {
    // Find if the hit object belongs to one of our blocks
    let hitObject = intersects[0].object;
    let blockIndex = -1;
    
    // Traverse up to find the main mesh that we stored in our blocks array
    while (hitObject && blockIndex === -1) {
      blockIndex = blocks.findIndex(b => b.mesh === hitObject);
      if (blockIndex === -1) hitObject = hitObject.parent;
    }

    if (blockIndex !== -1) {
      const b = blocks[blockIndex];
      scene.remove(b.mesh);
      blocks.splice(blockIndex, 1);
      score.value++;
      
      // Flash effect or some feedback
    }
  }
};

const animate = () => {
  animationId = requestAnimationFrame(animate);

  if (gameStarted.value && !gameOver.value) {
    // Spawning logic - gradually gets faster
    const spawnRate = Math.max(20, 60 - Math.floor(score.value / 5));
    if (frameCount % spawnRate === 0) createBlock();

    const speed = BASE_SPEED + (score.value * 0.002);

    for (let i = blocks.length - 1; i >= 0; i--) {
      const b = blocks[i];
      b.mesh.position.z += speed;
      b.mesh.rotation.y += 0.02;
      b.mesh.rotation.x += 0.01;

      // Fail condition: Block escaped past the camera
      if (b.mesh.position.z > KILL_Z) {
        gameOver.value = true;
        if (score.value > highScore.value) {
          highScore.value = score.value;
          localStorage.setItem('patronian_highscore', score.value);
          isNewRecord.value = true;
        }
      }
    }
    frameCount++;
  }

  renderer.render(scene, camera);
};

onMounted(() => {
  const saved = localStorage.getItem('patronian_highscore');
  if (saved) highScore.value = parseInt(saved);
  setupScene();
  animate();
});

onUnmounted(() => {
  cancelAnimationFrame(animationId);
  renderer.dispose();
});
</script>

<template>
  <div class="fixed inset-0 z-[100] flex items-center justify-center bg-patronian-black/90 backdrop-blur-xl">
    <div class="relative p-8 border border-patronian-gold/30 bg-patronian-black glow-gold">
      <div class="flex justify-between items-center mb-6">
        <div>
          <div class="text-[10px] uppercase tracking-widest text-patronian-gold font-bold">Protocol: DATA_PURGE_3D</div>
          <div class="text-2xl font-bold font-mono text-white">INTERCEPTED: {{ score }}</div>
        </div>
        <button @click="$emit('close')" class="text-patronian-gold hover:text-white transition-colors uppercase text-xs font-bold tracking-widest">
          Terminate [X]
        </button>
      </div>

      <div 
        ref="containerRef" 
        @mousedown="handleClick"
        class="bg-patronian-black border border-patronian-white/10 cursor-crosshair overflow-hidden"
        style="width: 400px; height: 500px;"
      ></div>

      <div v-if="!gameStarted && !gameOver" class="absolute inset-x-8 top-1/2 -translate-y-1/2 text-center pointer-events-none">
        <div class="text-white font-mono animate-pulse tracking-widest">SMASH MOVING DATA BLOCKS</div>
        <div class="text-patronian-gold text-[10px] uppercase mt-2">Don't let them breach the perimeter</div>
      </div>

      <div v-if="gameOver" class="absolute inset-x-8 top-1/2 -translate-y-1/2 p-8 bg-patronian-gold text-patronian-black text-center space-y-4 shadow-[0_0_50px_rgba(212,175,55,0.5)]">
        <h2 class="text-3xl font-bold uppercase tracking-tighter italic">FIREWALL BREACHED</h2>
        <div class="space-y-1">
          <p class="text-[10px] uppercase font-bold opacity-70">Final Score</p>
          <p class="text-4xl font-black font-mono tracking-tighter">{{ score }}</p>
        </div>
        <div class="border-t border-patronian-black/20 pt-4 flex justify-between items-center px-4">
          <div class="text-left">
            <p class="text-[10px] uppercase font-bold opacity-70">Global Best</p>
            <p class="text-xl font-bold font-mono">{{ highScore }}</p>
          </div>
          <div v-if="isNewRecord" class="bg-patronian-black text-patronian-gold px-3 py-1 text-[10px] font-bold uppercase animate-bounce">
            New Record!
          </div>
        </div>
        <button @click="initGame" class="w-full py-3 bg-patronian-black text-patronian-gold font-bold uppercase tracking-widest hover:bg-patronian-white transition-colors mt-2">
          RESTORE BACKUP
        </button>
      </div>

      <div class="mt-4 text-[10px] text-gray-500 flex justify-between uppercase font-mono tracking-widest leading-relaxed">
        <span>RENDER: WEBGL_CORE</span>
        <span>OBJECTIVE: CLICK TO NEUTRALIZE</span>
      </div>
    </div>
  </div>
</template>
