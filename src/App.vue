<script setup lang="ts">
import { ref } from 'vue';
import RetroBackground from './components/RetroBackground.vue';
import About from './components/About.vue';
import Experience from './components/Experience.vue';
import Education from './components/Education.vue';
import Skills from './components/Skills.vue';

const currentSection = ref('HOME');

const setSection = (section: string) => {
  currentSection.value = section;
};
</script>

<template>
  <main class="retro-container">
    <div class="bg-wrapper">
      <RetroBackground />
    </div>
    <div class="bros-container">
      <img src="/bros.png" alt="The Bros" class="bros-img" />
    </div>
    <div class="crs-overlay"></div>
    <div class="game-wrapper">
      
      <header class="hero">
        <h1 class="glitch-text">AVIRUKTH</h1>
        <h2 class="role-text">&lt; DATA ENGINEER /&gt;</h2>
      </header>

      <!-- Top Navigation Bar -->
      <nav class="top-nav">
        <button @click="setSection('HOME')" :class="{ active: currentSection === 'HOME' }">HOME</button>
        <button @click="setSection('ABOUT')" :class="{ active: currentSection === 'ABOUT' }">ABOUT</button>
        <button @click="setSection('EXPERIENCE')" :class="{ active: currentSection === 'EXPERIENCE' }">EXPERIENCE</button>
        <button @click="setSection('EDUCATION')" :class="{ active: currentSection === 'EDUCATION' }">EDUCATION</button>
        <button @click="setSection('SKILLS')" :class="{ active: currentSection === 'SKILLS' }">SKILLS</button>
      </nav>

      <section class="screen-content">
        <div class="content-scroll-area">
          <About v-if="currentSection === 'ABOUT'" />
          <Experience v-if="currentSection === 'EXPERIENCE'" />
          <Education v-if="currentSection === 'EDUCATION'" />
          <Skills v-if="currentSection === 'SKILLS'" />
        </div>
      </section>
      
    </div>
  </main>
</template>

<style scoped>
.retro-container {
  display: flex;
  flex-direction: column;
  height: 100vh;
  width: 100vw;
  overflow: hidden;
  background-color: #000;
  position: relative;
}

.bg-wrapper {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 1;
}

.bros-container {
  position: absolute;
  bottom: -15vh; /* Crop bottom 15-20% */
  left: 50%;
  transform: translateX(-50%);
  z-index: 2; /* Behind the game wrapper (content) */
  pointer-events: none;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: flex-end;
}

/* Bros Image - standard opacity */
.bros-img {
  width: 100%;
  height: auto;
  max-width: 1200px;
  max-height: 85vh; 
  object-fit: cover;
  filter: drop-shadow(0 0 20px rgba(0,0,0,0.5)) brightness(1.2); 
  opacity: 1;
}

/* Removed Hologram Animation */
.hologram {
  display: none; 
}

@keyframes scanline {
  0% { background-position: 0 0; }
  100% { background-position: 0 100%; }
}

@keyframes flicker {
  0%, 100% { opacity: 0.8; }
  50% { opacity: 0.75; }
}

.crs-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(
    rgba(18, 16, 16, 0) 50%,
    rgba(0, 0, 0, 0.25) 50%
  );
  background-size: 100% 4px;
  pointer-events: none;
  z-index: 10;
}

.game-wrapper {
  display: flex;
  flex-direction: column;
  height: 100%;
  width: 100%;
  max-width: 100%; /* Full width */
  margin: 0;
  padding: 0; /* Full bleed */
  box-sizing: border-box;
  z-index: 20; /* Move ABOVE CRT overlay for clear text */
  position: relative;
  pointer-events: none; /* Allow clicks to pass through to background */
}

header {
  flex-shrink: 0;
  pointer-events: none;
}

/* Hero Styles */
.hero {
  text-align: center;
  width: 100%;
  margin-top: 4vh;    /* Move to top */
  padding-top: 0;     /* Remove large padding */
  z-index: 25;        /* Ensure above everything */
  pointer-events: none;
}

h1.glitch-text {
  font-family: var(--font-primary);
  font-size: 5rem;
  margin-bottom: 0;
  color: #000; /* Black fill for outlined look, or just Yellow */
  /* Star Wars Style: Yellow with Black Outline */
  color: var(--color-heading);
  -webkit-text-stroke: 2px #000;
  text-shadow: 0 0 10px rgba(0, 0, 0, 0.8), 0 0 20px rgba(255, 232, 31, 0.3);
  letter-spacing: 0.2rem;
  text-transform: uppercase;
  font-weight: 900;
}

h2.role-text {
  font-family: var(--font-primary);
  font-size: 1.5rem;
  color: var(--color-text);
  margin-top: 0.5rem;
  margin-bottom: 1rem; /* Reduced further for tight layout */
  letter-spacing: 0.3rem;
  text-transform: uppercase;
  font-weight: 500;
}

/* Top Navigation Bar */
.top-nav {
  flex-shrink: 0;
  display: flex;
  justify-content: center;
  gap: 1rem;
  padding: 0.5rem;
  margin-bottom: 1rem;
  z-index: 30;
  pointer-events: auto; /* Enable clicks */
}

/* Datapad UI - Screen Content */
.screen-content {
  flex: 1; /* Grow to fill remaining space */
  display: flex;
  justify-content: flex-start;
  align-items: center;
  overflow: hidden;
  position: relative;
  
  /* Removed Glassmorphism */
  background: transparent;
  backdrop-filter: none;
  -webkit-backdrop-filter: none;
  
  border-top: none;
  border-bottom: none;
  border-radius: 0;
  box-shadow: none;
  margin-bottom: 0;
}

.content-scroll-area {
  width: 100%;
  height: 100%;
  overflow-y: auto;
  padding: 1rem; /* Compact padding */
  scrollbar-width: thin;
  scrollbar-color: rgba(75, 213, 238, 0.5) transparent;
  pointer-events: auto; /* Enable scrolling/selection */
}

/* Custom Scrollbar */
.content-scroll-area::-webkit-scrollbar {
  width: 6px;
}
.content-scroll-area::-webkit-scrollbar-track {
  background: transparent;
}
.content-scroll-area::-webkit-scrollbar-thumb {
  background-color: rgba(75, 213, 238, 0.5); /* Hologram blue */
  border-radius: 10px;
}

button {
  font-family: inherit;
  font-size: 0.9rem; /* Slightly larger for main nav */
  cursor: pointer;
  text-transform: uppercase;
  transition: all 0.1s;
  box-shadow: 0 4px 0 #000;
  min-width: 100px;
  background: #222;
  color: #fff;
  border: 1px solid #555;
  padding: 10px 16px;
}

button:active {
  transform: translateY(4px);
  box-shadow: 0 0 0 #000;
}

button:hover {
  background: #333;
  border-color: #777;
}

button.active {
  background: #ff0000;
  border-color: #ff9999;
  color: white;
  box-shadow: 0 4px 0 #990000;
  text-shadow: 1px 1px 0 #000;
}

button.active:active {
  box-shadow: 0 0 0 #990000;
}

@keyframes chomp {
  0% { transform: rotate(0deg); }
  50% { transform: rotate(45deg); }
  100% { transform: rotate(0deg); }
}

@media (max-width: 600px) {
  h1.glitch-text {
    font-size: 2.2rem; /* Smaller for mobile */
    letter-spacing: 0.1rem;
  }
  
  h2.role-text {
    font-size: 1rem;
    letter-spacing: 0.1rem;
  }
  
  .top-nav {
    flex-wrap: wrap; /* Allow wrapping on small screens */
    gap: 0.5rem;
    padding: 0.5rem 1rem;
  }
  
  button {
    padding: 8px 12px;
    font-size: 0.75rem;
    min-width: 80px;
    flex: 1 0 auto; /* Allow buttons to grow slightly to fill rows */
  }

  .bros-container {
    bottom: -5vh;
    opacity: 0.4; /* Slightly more visible */
  }

  .bros-img {
    /* Zoom in on mobile */
    min-width: 150%; 
    width: auto;
    height: 50vh;
    max-width: none; 
  }
  
  .content-scroll-area {
    padding: 1rem 0.5rem; /* Maximize width */
  }
}
</style>
