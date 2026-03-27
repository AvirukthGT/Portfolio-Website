<script setup lang="ts">
const skills = [
  "Data Build Tool (DBT)",
  "Snowflake",
  "Amazon Web Services (AWS)",
  "Machine Learning",
  "ETL/ELT Pipelines",
  "Data Infrastructure",
  "Statistical Modeling",
  "Python",
  "SQL",
  "Quantitative Finance"
];

const certifications = [
  "Stanford Machine Learning Specialization",
  "IBM Data Analyst Professional Certificate"
];
</script>

<template>
  <section class="skills-section">
    <div class="container">
      <div class="panel left">
        <h3 class="panel-title">INVENTORY / SKILLS</h3>
        <ul class="skill-list">
          <li v-for="skill in skills" :key="skill">
            <span class="bullet">></span> {{ skill }}
          </li>
        </ul>
      </div>
      
      <div class="panel right">
        <h3 class="panel-title">ACHIEVEMENTS</h3>
        <ul class="cert-list">
          <li v-for="cert in certifications" :key="cert">
            <div class="trophy">🏆</div>
            <span>{{ cert }}</span>
          </li>
        </ul>
      </div>
    </div>
  </section>
</template>

<style scoped>
.skills-section {
  width: 100%;
  max-width: 900px;
  margin: 4rem auto;
  padding: 0 1rem;
}

.container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2rem;
}

.panel {
  background: #111;
  border: 1px solid #333;
  padding: 1.5rem;
}

.panel:hover {
  border-color: #555;
}

.panel-title {
  color: #fff;
  border-bottom: 1px solid #333;
  padding-bottom: 0.5rem;
  margin-bottom: 1rem;
  font-size: 1rem;
  letter-spacing: 2px;
}

.skill-list, .cert-list {
  list-style: none;
  padding: 0;
}

.skill-list li {
  color: white;
  margin-bottom: 0.8rem;
  font-size: 0.9rem;
  display: flex;
  align-items: center;
  gap: 10px;
}

.bullet {
  color: #fff;
}

.cert-list li {
  display: flex;
  align-items: flex-start;
  gap: 10px;
  color: white;
  margin-bottom: 1rem;
  font-size: 0.9rem;
}

.trophy {
  font-size: 1.2rem;
}

@media (max-width: 768px) {
  .container {
    grid-template-columns: 1fr;
  }
}
</style>
