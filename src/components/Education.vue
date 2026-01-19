<script setup lang="ts">
interface Education {
  school: string;
  degree: string;
  period: string;
}

const education: Education[] = [
  {
    school: "Monash University",
    degree: "Master of Data Science, Information Technology",
    period: "Feb 2024 - Nov 2025"
  },
  {
    school: "Nitte Meenakshi Institute of Technology",
    degree: "Bachelor of Engineering - BE, Computer Science",
    period: "Aug 2019 - July 2023"
  }
];
</script>

<template>
  <section class="education-section">
    <h3 class="section-title">TRAINING HISTORY</h3>
    
    <div class="grid">
      <div v-for="(edu, index) in education" :key="index" class="edu-card">
        <div class="icon">🎓</div>
        <h4>{{ edu.school }}</h4>
        <p class="degree">{{ edu.degree }}</p>
        <p class="period">{{ edu.period }}</p>
      </div>
    </div>
  </section>
</template>

<style scoped>
.education-section {
  width: 100%;
  max-width: 800px;
  margin: 4rem auto;
}

.section-title {
  text-align: center;
  color: var(--color-heading);
  font-size: 1.5rem;
  margin-bottom: 2rem;
  letter-spacing: 2px;
  text-shadow: 0 0 10px rgba(255, 232, 31, 0.5);
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); /* Narrower min-width */
  gap: 2rem;
  padding: 0 1rem;
}

@media (max-width: 600px) {
  .grid {
    grid-template-columns: 1fr; /* Force stack on small screens */
    padding: 0;
  }
  
  .edu-card {
    padding: 1.5rem;
  }
}

.edu-card {
  background: #000; /* Solid Black */
  border: 2px solid var(--color-text);
  padding: 2rem;
  text-align: center;
  position: relative;
  overflow: hidden;
  box-shadow: 0 0 10px rgba(75, 213, 238, 0.1);
  transition: all 0.3s ease;
}

.edu-card:hover {
  border-color: var(--color-heading);
  transform: translateY(-5px);
  box-shadow: 0 0 20px rgba(255, 232, 31, 0.2);
}

/* Scanline removed for readability */
.icon {
  font-size: 2rem;
  margin-bottom: 1rem;
  text-shadow: 0 0 10px var(--color-text);
}

.icon {
  font-size: 2rem;
  margin-bottom: 1rem;
}

h4 {
  color: var(--vt-c-white);
  margin-bottom: 0.5rem;
  font-size: 1rem;
}

.degree {
  color: #aaa;
  font-size: 0.8rem;
  margin-bottom: 0.5rem;
}

.period {
  color: #00ffff;
  font-size: 0.7rem;
}

@keyframes scanline {
  0% { transform: translateY(-100%); }
  100% { transform: translateY(200px); } /* Approximate height of card */
}
</style>
