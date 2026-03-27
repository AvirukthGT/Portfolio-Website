<script setup lang="ts">
import { ref, shallowRef, onMounted, onUnmounted, watch } from 'vue';
import { GLTFModel, OrbitControls } from '@tresjs/cientos';
import TieFighter from './TieFighter.vue';

// Greetings Array
const greetings = ['Hello', 'Hola', 'Namaskar', 'Hej', 'Bonjour', 'Ciao', 'Konnichiwa'];
const currentGreeting = ref(greetings[0]);
const activeModel = ref<'vader' | 'maul'>('vader');
let greetingIndex = 0;
let greetingInterval: number;

// Scroll & 3D Camera Logic
const cameraZ = shallowRef(15); // Initial zoom
const baseZ = 15;
const maxZ = 35; // How far it can zoom out (limit so it doesn't become too small)

const handleScroll = () => {
  const scrollPos = window.scrollY;
  // Slower zoom-out calculation so it gently moves away
  const zoomFactor = scrollPos * 0.05; 
  let newZ = baseZ + zoomFactor;
  if (newZ > maxZ) newZ = maxZ;
  
  // Disabled zoom out on scroll as requested by user
  // cameraZ.value = newZ;

  // Determine which section we are in based on scroll position to swap models
  const projectsEl = document.getElementById('projects');
  if (projectsEl) {
    // If we scrolled past the start of the Projects section (with a little offset)
    const threshold = projectsEl.offsetTop - window.innerHeight / 2;
    if (scrollPos >= threshold) {
      activeModel.value = 'maul';
    } else {
      activeModel.value = 'vader';
    }
  }
};

onMounted(() => {
  // Rotate Greetings
  greetingInterval = setInterval(() => {
    greetingIndex = (greetingIndex + 1) % greetings.length;
    currentGreeting.value = greetings[greetingIndex];
  }, 2000);

  // Attach Scroll Listener to window since we moved to single page
  window.addEventListener('scroll', handleScroll);
});

onUnmounted(() => {
  clearInterval(greetingInterval);
  window.removeEventListener('scroll', handleScroll);
});
</script>

<template>
  <div class="hero-scroll-container">
    <!-- 3D Background - completely decoupled from text flow -->
    <div class="canvas-wrapper">
      <TresCanvas clear-color="#000000">
        <TresPerspectiveCamera :position="[0, 1.5, cameraZ]" :look-at="[0, 1, 0]" />
        
        <TresAmbientLight :intensity="2" />
        <TresDirectionalLight :position="[2, 5, 5]" :intensity="3" />
        <TresDirectionalLight :position="[-5, -2, -5]" :intensity="1" color="#ff0000" />
        
        <OrbitControls :enable-zoom="false" :enable-pan="false" />
        
        <Suspense>
          <TresGroup>
            <!-- Darth Vader: Center/Right -->
            <TresGroup v-if="activeModel === 'vader'" :position="[0, -6, 0]" :rotation="[0, Math.PI / 6, 0]">
              <GLTFModel path="/models/darth_vader_by_makeamo.glb" :scale="[0.05, 0.05, 0.05]" />
            </TresGroup>
            
            <!-- Darth Maul: On the Left -->
            <TresGroup v-if="activeModel === 'maul'" :position="[-1, -6, -2]" :rotation="[0, Math.PI / 4, 0]">
              <GLTFModel path="/models/darth_maul_new.glb" :scale="[6, 6, 6]" />
            </TresGroup>

            <!-- TIE Fighter: Flying in the background -->
            <TieFighter />
          </TresGroup>
        </Suspense>
      </TresCanvas>
    </div>

    <!-- Foreground Content - scrolls normally within the hero-scroll-container -->
    <div class="overlay-inner">
      <div class="hero-content">
        <div class="greeting-wrapper">
          <transition name="fade-slide" mode="out-in">
            <h1 :key="currentGreeting" class="greeting-text">{{ currentGreeting }}</h1>
          </transition>
        </div>
        
        <h2 class="main-heading">
          I'm Avi,<br/>
          I build and maintain pipelines
        </h2>
      </div>
    </div>
  </div>
</template>

<style scoped>
.hero-scroll-container {
  width: 100%;
  position: relative;
  /* Occupy the full initial viewport (minus navbar) */
  height: calc(100vh - 80px);
  display: flex;
  align-items: center;  /* Vertically center the text */
  justify-content: flex-start; /* Align text to the left */
}

/* 3D Canvas stays locked to the screen background */
.canvas-wrapper {
  position: fixed;
  top: 80px; /* Offset for navbar */
  left: 0;
  width: 100vw;
  height: calc(100vh - 80px);
  z-index: -10; /* Keep it behind everything */
  pointer-events: none; /* Let clicks pass through */
}

/* Constrain the text to the same max-width as the rest of the site */
.overlay-inner {
  width: 100%;
  max-width: 1100px;
  margin: 0 auto;
  height: 100%;
  display: flex;
  align-items: center; /* Vertically center the text container */
}

.hero-content {
  position: relative;
  z-index: 10;
  max-width: 800px;
  pointer-events: auto;
  padding-left: clamp(1.5rem, 5vw, 3rem); /* Match App.vue padding */
}

.greeting-wrapper {
  min-height: 4.5rem; /* Reserve space so layout doesn't jump */
  margin-bottom: 1rem;
}

.greeting-text {
  font-family: var(--font-primary);
  font-size: clamp(2.5rem, 5vw, 4rem); /* Fluid scaling based on viewport width */
  font-weight: 700;
  color: #fff;
  margin: 0;
}

.main-heading {
  font-family: var(--font-primary);
  font-size: clamp(1.2rem, 3vw, 2rem); /* Fluid scaling based on viewport width */
  font-weight: 400;
  color: #ccc;
  line-height: 1.5;
  margin: 0;
}

/* Greeting Animation */
.fade-slide-enter-active,
.fade-slide-leave-active {
  transition: all 0.5s ease;
}

.fade-slide-enter-from {
  opacity: 0;
  transform: translateY(20px);
}

.fade-slide-leave-to {
  opacity: 0;
  transform: translateY(-20px);
}
</style>
