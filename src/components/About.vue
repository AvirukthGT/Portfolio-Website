<script setup lang="ts">
</script>

<template>
  <section class="about-section">
    <div class="star-wars-panel">
      <h3>PLAYER BIO</h3>
      <div class="content">
        <p>
          Data Engineer with a Master of Data Science and a specialized focus on building infrastructure for quantitative finance. 
          My background in machine learning and statistical modeling allows me to design data systems that aren't just scalable, 
          but specifically optimized for the needs of financial analysis and algorithmic trading.
        </p>
        <p>
          I specialize in constructing efficient, low-latency pipelines that power quantitative systems and enable real-time data driven decision making.
        </p>
        <p>
          Outside of engineering, I am disciplined about fitness and can be found at the gym. 
          I am also an active investor in the stock market, constantly refining my own strategies and expanding my financial portfolio.
          I am always looking to connect with others at the intersection of data engineering and finance.
        </p>
      </div>
    </div>
  </section>
</template>

<style scoped>
.about-section {
  width: 100%;
  max-width: 800px;
  margin: 1rem auto; /* Tighten up margin */
  padding: 0 1rem;
}

/* Content specific overrides if needed, otherwise inherit from global .star-wars-panel */
.content p {
  margin-bottom: 1.5rem;
  color: #fff; /* Crisp white for reading */
  font-size: 1rem;
  line-height: 1.8;
}

.content p:last-child {
  margin-bottom: 0;
}
</style>
