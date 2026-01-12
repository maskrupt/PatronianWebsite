<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import * as THREE from 'three';

const containerRef = ref(null);
let scene, camera, renderer, object, particles;
let animationId;

const initThree = () => {
  scene = new THREE.Scene();
  
  const width = containerRef.value.clientWidth;
  const height = containerRef.value.clientHeight;
  
  camera = new THREE.PerspectiveCamera(75, width / height, 0.1, 1000);
  camera.position.z = 5;

  renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
  renderer.setSize(width, height);
  renderer.setPixelRatio(window.devicePixelRatio);
  containerRef.value.appendChild(renderer.domElement);

  // Geometry: A complex tech-looking polyhedron
  const geometry = new THREE.IcosahedronGeometry(2, 2);
  const material = new THREE.MeshPhongMaterial({
    color: 0xd4af37,
    wireframe: true,
    transparent: true,
    opacity: 0.4,
    emissive: 0xd4af37,
    emissiveIntensity: 0.5
  });
  
  object = new THREE.Mesh(geometry, material);
  scene.add(object);

  // Inner solid core
  const coreGeo = new THREE.IcosahedronGeometry(1.5, 0);
  const coreMat = new THREE.MeshPhongMaterial({
    color: 0xffffff,
    emissive: 0xffffff,
    emissiveIntensity: 0.2,
    transparent: true,
    opacity: 0.1
  });
  const core = new THREE.Mesh(coreGeo, coreMat);
  scene.add(core);

  // Particles
  const pointsGeometry = new THREE.BufferGeometry();
  const count = 500;
  const positions = new Float32Array(count * 3);
  for (let i = 0; i < count * 3; i++) {
    positions[i] = (Math.random() - 0.5) * 15;
  }
  pointsGeometry.setAttribute('position', new THREE.BufferAttribute(positions, 3));
  const pointsMaterial = new THREE.PointsMaterial({
    color: 0xffffff,
    size: 0.05,
    transparent: true,
    opacity: 0.5
  });
  particles = new THREE.Points(pointsGeometry, pointsMaterial);
  scene.add(particles);

  // Lights
  const light = new THREE.PointLight(0xd4af37, 2, 50);
  light.position.set(5, 5, 5);
  scene.add(light);
  scene.add(new THREE.AmbientLight(0xffffff, 0.3));

  const animate = () => {
    animationId = requestAnimationFrame(animate);
    
    object.rotation.y += 0.005;
    object.rotation.x += 0.002;
    particles.rotation.y -= 0.001;
    
    renderer.render(scene, camera);
  };

  animate();
};

const handleResize = () => {
  if (!containerRef.value) return;
  const width = containerRef.value.clientWidth;
  const height = containerRef.value.clientHeight;
  renderer.setSize(width, height);
  camera.aspect = width / height;
  camera.updateProjectionMatrix();
};

onMounted(() => {
  initThree();
  window.addEventListener('resize', handleResize);
});

onUnmounted(() => {
  window.removeEventListener('resize', handleResize);
  cancelAnimationFrame(animationId);
  renderer.dispose();
});
</script>

<template>
  <div ref="containerRef" class="w-full h-full"></div>
</template>
