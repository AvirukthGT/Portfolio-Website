<script setup lang="ts">
// Simple Contact component
</script>

<template>
  <div class="contact-container">
    <h2>Contact</h2>
    <div class="contact-info">
      <p>Feel free to reach out to me for any inquiries or collaboration opportunities.</p>
      
      <div class="contact-links">
        <a href="mailto:avirukth@example.com" class="contact-link">
          <span class="label">Email:</span> avirukth@example.com
        </a>
        <a href="https://linkedin.com/in/avirukth" target="_blank" class="contact-link">
          <span class="label">LinkedIn:</span> linkedin.com/in/avirukth
        </a>
        <a href="https://github.com/avirukth" target="_blank" class="contact-link">
          <span class="label">GitHub:</span> github.com/avirukth
        </a>
      </div>
    </div>
  </div>
</template>

<style scoped>
.contact-container {
  padding: 2rem 0;
  width: 100%;
}

h2 {
  font-family: var(--font-primary);
  font-size: clamp(1.5rem, 4vw, 2rem); /* Fluid section title */
  margin-bottom: 2rem;
  border-bottom: 1px solid rgba(255, 255, 255, 0.2);
  padding-bottom: 0.5rem;
  text-transform: uppercase;
  letter-spacing: 0.1em;
}

.contact-info p {
  color: rgba(255, 255, 255, 0.7);
  margin-bottom: 2rem;
  line-height: 1.6;
  font-size: clamp(1rem, 2.5vw, 1.1rem); /* Fluid paragraph text */
}

.contact-links {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.contact-link {
  display: flex;
  align-items: center;
  gap: 1rem;
  color: #fff;
  text-decoration: none;
  font-size: clamp(0.9rem, 2vw, 1.1rem); /* Fluid link text */
  padding: 1rem;
  border: 1px solid rgba(255, 255, 255, 0.1);
  background-color: rgba(255, 255, 255, 0.02);
  border-radius: 4px;
  transition: border-color 0.2s ease, background-color 0.2s ease;
}

.contact-link:hover {
  border-color: rgba(255, 255, 255, 0.4);
  background-color: rgba(255, 255, 255, 0.05);
}

.label {
  opacity: 0.5;
  min-width: 80px;
}
</style>
