<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue';
import Hero from './components/Hero.vue';
import About from './components/About.vue';
import Experience from './components/Experience.vue';
import Projects from './components/Projects.vue';
import Contact from './components/Contact.vue';

const currentSection = ref('HOME');

const setSection = (section: string) => {
  currentSection.value = section;
  const element = document.getElementById(section.toLowerCase());
  if (element) {
    // Scroll the window to the element
    window.scrollTo({
      top: element.offsetTop,
      behavior: 'smooth'
    });
  }
};

const handleScroll = () => {
  const scrollPos = window.scrollY;
  const sections = ['home', 'about', 'experience', 'projects', 'contact'];
  
  for (const sec of sections) {
    const el = document.getElementById(sec);
    if (el) {
      // If scroll position is past the element's top minus offset
      const offsetTop = el.offsetTop - 100;
      if (scrollPos >= offsetTop) {
        currentSection.value = sec.toUpperCase();
      }
    }
  }
};

onMounted(() => {
  window.addEventListener('scroll', handleScroll);
});

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll);
});
</script>

<template>
  <main class="page">
    <!-- Minimalist Navbar -->
    <nav class="navbar">
      <div class="nav-name">Avirukth Gurulingegowda Thadaklur</div>
      <div class="nav-links">
        <a @click="setSection('ABOUT')" :class="{ active: currentSection === 'ABOUT' }">About</a>
        <a @click="setSection('EXPERIENCE')" :class="{ active: currentSection === 'EXPERIENCE' }">Experience</a>
        <a @click="setSection('PROJECTS')" :class="{ active: currentSection === 'PROJECTS' }">Projects</a>
        <a @click="setSection('CONTACT')" :class="{ active: currentSection === 'CONTACT' }">Contact</a>
      </div>
    </nav>

    <!-- Content -->
    <section class="content">
      <!-- Home section (Canvas is fixed inside Hero component) -->
      <div id="home">
        <Hero />
      </div>

      <!-- Other sections have inner padding -->
      <div id="about" class="content-inner">
        <About />
      </div>
      <div id="experience" class="content-inner">
        <Experience />
      </div>
      <div id="projects" class="content-inner">
        <Projects />
      </div>
      <div id="contact" class="content-inner">
        <Contact />
      </div>
    </section>
  </main>
</template>

<style scoped>
.page {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  width: 100%;
  background-color: #000;
  color: #fff;
}

.navbar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: clamp(1rem, 2vw, 1.25rem) clamp(1.5rem, 5vw, 3rem); /* Fluid navbar padding */
  flex-shrink: 0;
  position: relative;
  z-index: 100;
}

.nav-name {
  font-family: var(--font-primary);
  font-size: 1rem;
  font-weight: 600;
  letter-spacing: 0.02em;
  color: #fff;
  white-space: nowrap;
}

.nav-links {
  display: flex;
  gap: clamp(1rem, 3vw, 2.5rem); /* Fluid link gap */
}

.nav-links a {
  font-family: var(--font-primary);
  font-size: 0.85rem;
  color: rgba(255, 255, 255, 0.5);
  cursor: pointer;
  letter-spacing: 0.05em;
  text-transform: none;
  text-decoration: none;
  transition: color 0.2s ease;
}

.nav-links a:hover,
.nav-links a.active {
  color: #fff;
}

/* ── Content ── */
.content {
  width: 100%;
  position: relative;
  z-index: 1; /* Content sits cleanly above the 3D background */
}

.content-inner {
  width: 100%;
  max-width: 1100px;
  margin: 0 auto;
  padding: clamp(2rem, 5vw, 4rem) clamp(1.5rem, 5vw, 3rem); /* Fluid responsive padding */
  /* Add a subtle dark gradient behind text so it's readable over the 3D model */
  background: radial-gradient(circle at center, rgba(0,0,0,0.6) 0%, transparent 100%);
  border-radius: 20px;
}

/* ── Scrollbar ── */
.content::-webkit-scrollbar {
  width: 4px;
}
.content::-webkit-scrollbar-track {
  background: transparent;
}
.content::-webkit-scrollbar-thumb {
  background-color: rgba(255, 255, 255, 0.15);
  border-radius: 10px;
}

/* ── Mobile ── */
@media (max-width: 768px) {
  .navbar {
    flex-direction: column;
    gap: 1rem;
    padding: 1rem 1.5rem;
    text-align: center;
  }

  .nav-links {
    gap: 1.5rem;
  }

  .nav-links a {
    font-size: 0.8rem;
  }

  .content-inner {
    padding: 2rem 1.5rem;
  }
}
</style>
