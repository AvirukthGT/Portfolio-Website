<script setup lang="ts">
</script>

<template>
  <main class="retro-container">
    <div class="game-wrapper">
      <header>
        <div class="score-board">
          <span>1UP</span>
          <span>HIGH SCORE</span>
          <span>002024</span>
        </div>
      </header>
      
      <section class="hero">
        <h1 class="glitch-text">AVIRUKTH</h1>
        <h2 class="role-text">&lt; DATA ENGINEER /&gt;</h2>
        
        <div class="pacman-animation">
          <div class="pacman"></div>
          <div class="dot"></div>
          <div class="dot"></div>
          <div class="dot"></div>
          <div class="ghost"></div>
        </div>
      </section>

      <footer class="insert-coin">
        <p>INSERT COIN TO CONTINUE</p>
      </footer>
    </div>
  </main>
</template>

<style scoped>
.retro-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  min-height: 80vh;
}

.game-wrapper {
  text-align: center;
  width: 100%;
}

.score-board {
  display: flex;
  justify-content: space-between;
  width: 100%;
  max-width: 600px;
  margin: 0 auto 4rem;
  color: #ff0000;
  font-size: 0.8rem;
}

h1.glitch-text {
  font-size: 3rem;
  margin-bottom: 1rem;
  color: #ffff00;
  text-shadow: 4px 4px 0px #0000ff;
}

h2.role-text {
  font-size: 1.2rem;
  color: #00ff00;
  margin-bottom: 4rem;
}

.pacman-animation {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 20px;
  margin: 2rem 0;
}

.pacman {
  position: relative;
  background: transparent;
  width: 0; 
  height: 0; 
  border-right: 20px solid transparent; 
  border-top: 20px solid #ffff00; 
  border-left: 20px solid #ffff00; 
  border-bottom: 20px solid #ffff00; 
  border-top-left-radius: 20px; 
  border-top-right-radius: 20px; 
  border-bottom-left-radius: 20px; 
  border-bottom-right-radius: 20px;
  animation: chomp 0.3s infinite;
}

.dot {
  width: 10px;
  height: 10px;
  background: #ffb897;
  border-radius: 50%;
}

.ghost {
  width: 30px;
  height: 30px;
  background: red;
  border-radius: 15px 15px 0 0;
  position: relative;
}

.ghost::before, .ghost::after {
  content: '';
  position: absolute;
  top: 10px;
  width: 8px;
  height: 8px;
  background: white;
  border-radius: 50%;
}

.ghost::before { left: 5px; }
.ghost::after { right: 5px; }

.insert-coin {
  margin-top: 5rem;
  animation: blink 1s infinite;
}

@keyframes chomp {
  0% { transform: rotate(0deg); }
  50% { transform: rotate(45deg); } /* Basic imitation */
  100% { transform: rotate(0deg); }
}

@keyframes blink {
  0%, 100% { opacity: 1; }
  50% { opacity: 0; }
}

@media (max-width: 600px) {
  h1.glitch-text {
    font-size: 2rem;
  }
}
</style>
