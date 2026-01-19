<script setup lang="ts">
import { shallowRef, onMounted, onUnmounted } from 'vue';
import { GLTFModel, Stars } from '@tresjs/cientos';

const modelRotation = shallowRef(0);
const rotX = shallowRef(0);
const rotZ = shallowRef(0);
const cameraZ = shallowRef(14);
let animationFrameId: number;

const animate = () => {
  const time = Date.now() * 0.001;
  
  // Rotate the ship on all axes for a tumble effect
  rotX.value += 0.002;
  modelRotation.value += 0.005; 
  rotZ.value += 0.001;
  
  // Gentle Zoom In/Out (Sine wave between 16 and 20 z-index)
  // Base 18 ensures we see the whole ship comfortably
  cameraZ.value = 18 + Math.sin(time * 0.5) * 2; 

  animationFrameId = requestAnimationFrame(animate);
};

onMounted(() => {
  animate();
});

onUnmounted(() => {
  cancelAnimationFrame(animationFrameId);
});
</script>

<template>
  <TresCanvas clear-color="#000000" window-size>
    <TresPerspectiveCamera
      :position="[0, 2, cameraZ]"
      :look-at="[0, 0, 0]"
    />
    
    <!-- Automatic Animation: No OrbitControls -->

    <!-- Hyperspace Stars (Background) -->
    <Stars :radius="100" :depth="50" :count="8000" :size="0.1" :size-attenuation="true" :speed="2" />
    
    <!-- Lighting -->
    <TresAmbientLight :intensity="3" />
    <TresDirectionalLight :position="[0, 2, 5]" :intensity="5" />
    <TresDirectionalLight :position="[-5, -2, 5]" :intensity="2" color="#0000ff" />
    <TresDirectionalLight :position="[5, -2, 5]" :intensity="2" color="#ffff00" />

    <Suspense>
      <!-- Group wrapper handles the rotation since GLTFModel prop support varies -->
      <TresGroup :rotation-x="rotX" :rotation-y="modelRotation" :rotation-z="rotZ">
        <GLTFModel path="/models/tyefighter.glb" :scale="[3, 3, 3]" :position="[0, 0, 0]" />
      </TresGroup>
    </Suspense>
  </TresCanvas>
</template>
