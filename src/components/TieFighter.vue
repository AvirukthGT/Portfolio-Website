<script setup lang="ts">
import { shallowRef } from 'vue';
import { useLoop } from '@tresjs/core';
import { GLTFModel } from '@tresjs/cientos';

const tieFighterRef = shallowRef();
const { onBeforeRender } = useLoop();

onBeforeRender(({ elapsed }) => {
  if (tieFighterRef.value) {
    // Fly left to right and back using a sine wave on the X axis
    // Amplitude is 20 (from -20 to 20), Speed is 0.5
    tieFighterRef.value.position.x = Math.sin(elapsed * 0.5) * 20;
    
    // Add a slight vertical bobbing motion on the Y axis
    tieFighterRef.value.position.y = 2 + Math.cos(elapsed * 2) * 0.5;
    
    // Add a slight banking tilt on the Z axis based on travel direction
    tieFighterRef.value.rotation.z = Math.cos(elapsed * 0.5) * -0.2;
  }
});
</script>

<template>
  <TresGroup ref="tieFighterRef" :position="[-20, 2, -10]" :scale="[1.5, 1.5, 1.5]">
    <GLTFModel path="/models/tyefighter.glb" />
  </TresGroup>
</template>
