<script setup lang="ts">
interface Job {
  company: string;
  role: string;
  period: string;
  description?: string;
}

const jobs: Job[] = [
  {
    company: "Monash University",
    role: "Data Engineer",
    period: "Aug 2025 - Nov 2025"
  },
  {
    company: "COSMIC365.AI",
    role: "Data Scientist",
    period: "Mar 2025 - July 2025"
  },
  {
    company: "Edutech",
    role: "Financial Analyst",
    period: "Aug 2023 - Oct 2023"
  },
  {
    company: "Data Glacier",
    role: "Data Scientist",
    period: "July 2023 - Aug 2023"
  }
];
</script>

<template>
  <section class="experience-section">
    <h3 class="section-title">QUEST LOG</h3>
    
    <div class="grid">
      <div v-for="(job, index) in jobs" :key="index" class="job-card">
        <div class="card-header">
          <span class="level-badge">LVL {{ jobs.length - index }}</span>
          <span class="period">{{ job.period }}</span>
        </div>
        <h4 class="company">{{ job.company }}</h4>
        <div class="role">{{ job.role }}</div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.experience-section {
  width: 100%;
  max-width: 1000px; /* Wider for grid */
  margin: 1rem auto;
  padding: 0 0.5rem;
}

.section-title {
  text-align: center;
  color: var(--color-heading);
  font-size: clamp(1.2rem, 3vw, 1.5rem); /* Fluid section title */
  margin-bottom: 1.5rem; /* Reduced */
  text-shadow: 0 0 10px rgba(255, 232, 31, 0.5);
}

.grid {
  display: grid;
  grid-template-columns: 1fr 1fr; /* 2 Columns */
  gap: 1.5rem;
}

.job-card {
  background: #000; /* Solid Black */
  border: 2px solid var(--color-text);
  padding: 1.25rem;
  transition: transform 0.2s;
  box-shadow: 0 0 10px rgba(75, 213, 238, 0.1);
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.job-card:hover {
  transform: translateY(-5px);
  border-color: var(--color-heading);
  box-shadow: 0 0 15px rgba(255, 232, 31, 0.2);
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 0.5rem;
}

.level-badge {
  background: var(--color-heading);
  color: #000;
  font-weight: bold;
  font-size: 0.7rem;
  padding: 2px 6px;
  border-radius: 2px;
}

.period {
  color: #888;
  font-size: 0.8rem;
}

.company {
  color: var(--color-heading);
  font-size: clamp(1rem, 2.5vw, 1.2rem); /* Fluid company name */
  margin-bottom: 0.2rem;
  text-transform: uppercase;
}

.role {
  color: #fff;
  font-size: clamp(0.9rem, 2vw, 1rem); /* Fluid role text */
}

@media (max-width: 768px) {
  .grid {
    grid-template-columns: 1fr; /* Stack on mobile */
  }
}
</style>
