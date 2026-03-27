<script setup lang="ts">
import { ref, computed } from 'vue';

const projects = ref([
  {
    title: 'MelPark',
    subtitle: 'Melbourne Real-Time Parking Data Engineering Pipeline',
    description: 'A robust, automated data pipeline implementing a modern Lakehouse Architecture to ingest real-time sensor data from the City of Melbourne Open Data Portal. Transforms raw sensor events into a structured Star Schema to provide insights into peak parking hours and high-demand zones.',
    github: 'https://github.com/AvirukthGT/MelPark.git',
    techStack: ['Azure Databricks', 'Apache Kafka', 'Debezium', 'dbt Core', 'Apache Airflow', 'Terraform', 'PowerBI'],
    features: [
      'Zero-lag CDC streaming with Debezium & PostgreSQL',
      'Medallion Architecture (Bronze -> Silver -> Gold)',
      'Infrastructure as Code via Terraform'
    ]
  },
  {
    title: 'AeroStream',
    subtitle: 'Real-Time Flight Efficiency Engine',
    description: 'An operational intelligence engine that fuses live flight telemetry (OpenSky API) with hyper-local atmospheric data (OpenMeteo). Uses a physics-aware Machine Learning model to calculate theoretical "Optimal Velocity" and generate live Efficiency Scores for aircraft.',
    github: 'https://github.com/AvirukthGT/AeroStream.git',
    techStack: ['FastAPI', 'Vue.js 3', 'Spark MLlib', 'Azure Data Factory', 'ADLS Gen2'],
    features: [
      'Decoupled MLOps Architecture (Training vs Inference)',
      'Spatio-Temporal Joins across moving aircraft/weather',
      'Interactive Leaflet.js Geospacial UI'
    ]
  },
  {
    title: 'Black Swan Detection Engine',
    subtitle: 'Real-Time Market Anomaly Platform',
    description: 'An end-to-end market intelligence platform designed to ingest, correlate, and visualize disparate data sources (Tick data + Global News + Reddit Sentiment) in real-time to identify "Pump/Dump" anomalies.',
    github: 'https://github.com/AvirukthGT/blackSwan-Market-Anamoly-Pipeline.git',
    techStack: ['Apache Kafka', 'Snowflake', 'dbt Core', 'FastAPI', 'Vue.js 3', 'Apache Airflow'],
    features: [
      'Live stream processing via Kafka & Snowpipe',
      'NLP Sentiment Analysis on Global News feeds',
      '"Retro-Cyberpunk" Trading Terminal UI'
    ]
  },
  {
    title: 'Revenue Optimization Engine',
    subtitle: 'Predictive Pricing Analytics Platform',
    description: 'A full-stack data platform engineered to solve the inefficiencies of static retail pricing. Integrates historical sales, real-time competitor pricing, and weather forecasts into a unified XGBoost model to recommend optimal price points.',
    github: 'https://github.com/AvirukthGT/revenue-optimization-engine.git',
    techStack: ['AWS S3', 'Snowflake', 'dbt Core', 'XGBoost', 'Reflex', 'FastAPI'],
    features: [
      'Temporal Data "Time Travel" Shifting Algorithm',
      'Monotonic constraints applied to XGBoost for economic safety',
      '"Storm Surge" Engine detecting weather-correlated demand'
    ]
  },
  {
    title: 'AWS Delta Stream Lakehouse',
    subtitle: 'End-to-End Event-Driven Data Lakehouse',
    description: 'A production-grade simulation of a modern E-Commerce Data Platform demonstrating an Event-Driven Lakehouse Architecture capable of ingesting transactional data, processing it incrementally via CDC, and serving real-time business insights to end-users.',
    github: 'https://github.com/AvirukthGT/aws-delta-stream-lakehouse.git',
    techStack: ['AWS RDS', 'Amazon S3', 'AWS Athena', 'AWS Glue', 'Terraform', 'Streamlit', 'Python', 'PostgreSQL'],
    features: [
      'Changes Data Capture (CDC) via Python & Boto3',
      'Medallion Architecture (Bronze -> Silver -> Gold)',
      'Serverless Compute querying via AWS Athena'
    ]
  },
  {
    title: 'NutriWarehouse Analytics Pipeline',
    subtitle: 'ApexLabs B2B & D2C Data Integration Pipeline',
    description: 'A unified analytics pipeline built on a Medallion Architecture that ingests, cleans, standardizes, and transforms B2B wholesale data into an existing D2C analytics environment following an acquisition.',
    github: 'https://github.com/AvirukthGT/apexlabs-analytics-pipeline.git',
    techStack: ['Databricks', 'Unity Catalog', 'Lakeflow Tasks', 'Apache Spark (PySpark)', 'AWS S3', 'Delta Lake'],
    features: [
      'Shared and conformed dimensional modeling',
      'Lakeflow Task pipeline orchestration',
      'Automated daily and full-load fact table aggregation'
    ]
  },
  {
    title: 'Sentinel',
    subtitle: 'Maritime Geopolitical Intelligence Platform',
    description: 'An end-to-end data engineering platform designed to track, quantify, and visualize the impact of geopolitical conflicts on global maritime supply chains using live AIS telemetry processed through a custom risk-scoring engine.',
    github: 'https://github.com/AvirukthGT/Marine-AIS-Tracker.git',
    techStack: ['GCP', 'Snowflake', 'dbt Core', 'Apache Airflow', 'FastAPI', 'React', 'Deck.gl', 'Docker'],
    features: [
      'Dark Fleet Detection identifying AIS spoofing/evasion',
      'Dynamic Cargo Value at Risk (VaR) Calculation',
      'Slowly Changing Dimensions (SCD2) for historical anomaly tracking'
    ]
  }
]);

// Pagination State
const currentPage = ref(1);
const itemsPerPage = 4;

const totalPages = computed(() => Math.ceil(projects.value.length / itemsPerPage));

const paginatedProjects = computed(() => {
  const start = (currentPage.value - 1) * itemsPerPage;
  const end = start + itemsPerPage;
  return projects.value.slice(start, end);
});

const nextPage = () => {
  if (currentPage.value < totalPages.value) {
    currentPage.value++;
    document.getElementById('projects')?.scrollIntoView({ behavior: 'smooth' });
  }
};

const prevPage = () => {
  if (currentPage.value > 1) {
    currentPage.value--;
    document.getElementById('projects')?.scrollIntoView({ behavior: 'smooth' });
  }
};
</script>

<template>
  <div class="projects-container">
    <h2 class="section-title">Projects</h2>
    
    <div class="project-grid">
      <transition-group name="project-fade" mode="out-in">
        <div v-for="(project, index) in paginatedProjects" :key="project.title" class="project-card">
          
          <div class="project-header">
          <h3>{{ project.title }}</h3>
          <span class="subtitle">{{ project.subtitle }}</span>
        </div>

        <p class="description">{{ project.description }}</p>

        <ul class="feature-list">
          <li v-for="(feature, idx) in project.features" :key="idx">
            {{ feature }}
          </li>
        </ul>

        <div class="tech-stack">
          <span v-for="tech in project.techStack" :key="tech" class="tech-badge">
            {{ tech }}
          </span>
        </div>

        <div class="card-footer">
          <a :href="project.github" target="_blank" rel="noopener noreferrer" class="github-btn">
            View on GitHub
            <svg xmlns="http://www.w3.org/O/svg/1.1" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"></path></svg>
          </a>
          </div>
        </div>
      </transition-group>
    </div>

    <!-- Pagination Controls -->
    <div class="pagination-controls" v-if="totalPages > 1">
      <button 
        class="page-btn" 
        @click="prevPage" 
        :disabled="currentPage === 1"
      >
        <svg xmlns="http://www.w3.org/O/svg/1.1" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="m15 18-6-6 6-6"/></svg>
        Previous
      </button>
      
      <div class="page-indicators">
        <span 
          v-for="page in totalPages" 
          :key="page" 
          class="page-dot"
          :class="{ active: page === currentPage }"
          @click="currentPage = page"
        ></span>
      </div>

      <button 
        class="page-btn" 
        @click="nextPage" 
        :disabled="currentPage === totalPages"
      >
        Next
        <svg xmlns="http://www.w3.org/O/svg/1.1" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="m9 18 6-6-6-6"/></svg>
      </button>
    </div>
  </div>
</template>

<style scoped>
.projects-container {
  padding: 2rem 0;
  width: 100%;
}

.section-title {
  font-family: var(--font-primary);
  font-size: clamp(2rem, 5vw, 2.5rem); /* Fluid section title */
  margin-bottom: 3rem;
  padding-bottom: 0.5rem;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: #fff;
  border-bottom: 2px solid rgba(255, 255, 255, 0.1);
  text-align: center;
}

.project-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
  gap: 2.5rem;
  min-height: 450px; /* Prevent layout jump during transition */
}

/* Transitions for project cards */
.project-fade-enter-active,
.project-fade-leave-active {
  transition: all 0.4s ease;
}
.project-fade-enter-from {
  opacity: 0;
  transform: translateY(20px);
}
.project-fade-leave-to {
  opacity: 0;
  transform: translateY(-20px);
}

.project-card {
  display: flex;
  flex-direction: column;
  background: rgba(15, 15, 15, 0.7);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 12px;
  padding: 2rem;
  transition: all 0.3s cubic-bezier(0.25, 0.8, 0.25, 1);
  position: relative;
  overflow: hidden;
}

/* Existing Card CSS removed for brevity below */

.project-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 4px;
  background: linear-gradient(90deg, #ff3366, #ff9933);
  opacity: 0;
  transition: opacity 0.3s ease;
}

.project-card:hover {
  transform: translateY(-5px);
  border-color: rgba(255, 255, 255, 0.3);
  box-shadow: 0 15px 35px rgba(0, 0, 0, 0.4);
}

.project-card:hover::before {
  opacity: 1;
}

.project-header {
  margin-bottom: 1.5rem;
}

.project-header h3 {
  font-family: var(--font-primary);
  font-size: clamp(1.4rem, 3.5vw, 1.75rem); /* Fluid project title */
  color: #fff;
  margin: 0 0 0.5rem 0;
  line-height: 1.2;
}

.subtitle {
  font-size: clamp(0.85rem, 2vw, 0.95rem); /* Fluid subtitle */
  color: #ff9933;
  font-weight: 500;
  letter-spacing: 0.05em;
  text-transform: uppercase;
}

.description {
  color: rgba(255, 255, 255, 0.8);
  font-size: clamp(0.9rem, 2vw, 1rem); /* Fluid description text */
  line-height: 1.6;
  margin-bottom: 1.5rem;
}

.feature-list {
  list-style-type: none;
  padding: 0;
  margin: 0 0 2rem 0;
}

.feature-list li {
  color: rgba(255, 255, 255, 0.7);
  font-size: clamp(0.85rem, 1.5vw, 0.9rem); /* Fluid feature list */
  margin-bottom: 0.5rem;
  padding-left: 1.5rem;
  position: relative;
  line-height: 1.4;
}

.feature-list li::before {
  content: '▹';
  position: absolute;
  left: 0;
  color: #ff3366;
}

.tech-stack {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-top: auto;
  margin-bottom: 2rem;
}

.tech-badge {
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.1);
  color: rgba(255, 255, 255, 0.9);
  padding: 0.3rem 0.8rem;
  border-radius: 20px;
  font-size: 0.75rem;
  font-family: monospace;
  letter-spacing: 0.05em;
  transition: background 0.2s ease;
}

.project-card:hover .tech-badge {
  background: rgba(255, 255, 255, 0.1);
}

.card-footer {
  display: flex;
  align-items: center;
  margin-top: 1rem;
  border-top: 1px solid rgba(255, 255, 255, 0.1);
  padding-top: 1.5rem;
}

.github-btn {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  color: #fff;
  text-decoration: none;
  font-size: 0.9rem;
  font-weight: 600;
  letter-spacing: 0.05em;
  transition: color 0.2s ease;
}

.github-btn svg {
  transition: transform 0.2s ease;
}

.github-btn:hover {
  color: #ff9933;
}

.github-btn:hover svg {
  transform: translateY(-2px);
}

/* ── Pagination Styling ── */
.pagination-controls {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 2rem;
  margin-top: 3rem;
  padding-top: 2rem;
  border-top: 1px solid rgba(255, 255, 255, 0.1);
}

.page-btn {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  background: transparent;
  border: 1px solid rgba(255, 255, 255, 0.2);
  color: #fff;
  padding: 0.5rem 1rem;
  border-radius: 4px;
  cursor: pointer;
  font-family: var(--font-primary);
  font-size: 0.9rem;
  letter-spacing: 0.05em;
  transition: all 0.2s ease;
}

.page-btn:hover:not(:disabled) {
  background: rgba(255, 255, 255, 0.1);
  border-color: #ff9933;
  color: #ff9933;
}

.page-btn:disabled {
  opacity: 0.3;
  cursor: not-allowed;
}

.page-indicators {
  display: flex;
  gap: 0.5rem;
}

.page-dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.2);
  cursor: pointer;
  transition: all 0.2s ease;
}

.page-dot.active {
  background: #ff3366;
  transform: scale(1.2);
}

.page-dot:hover:not(.active) {
  background: rgba(255, 255, 255, 0.5);
}

@media (max-width: 768px) {
  .project-grid {
    grid-template-columns: 1fr;
  }
  
  .section-title {
    font-size: 2rem;
  }
}
</style>
