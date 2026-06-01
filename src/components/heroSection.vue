<!-- components/HeroSection.vue -->
<template>
  <section class="hero">
    <div class="hero-container">
      <div class="hero-content">
        <div class="hero-badge">
          <span class="badge-dot"></span>
          <span class="badge-text">Since 2024</span>
        </div>

        <h1 class="hero-title">
          Taste the
          <span class="orange-text">Fusion</span>
          <br />
          of Global
          <span class="green-text">Flavors</span>
        </h1>

        <p class="hero-description">
          Experience a culinary journey where vibrant oranges meet fresh greens,
          wrapped in the deep teal of tradition and sprinkled with cyan stars of innovation.
        </p>

        <div class="hero-buttons">
          <button class="btn-orange">
            <span class="btn-icon">🍴</span>
            Explore Menu
          </button>
          <button class="btn-green">
            <span class="btn-icon">🥄</span>
            Book a Table
          </button>
        </div>

        <div class="hero-stats">
          <div class="stat">
            <div class="stat-number">50+</div>
            <div class="stat-label">Global Dishes</div>
          </div>
          <div class="stat-divider"></div>
          <div class="stat">
            <div class="stat-number">15+</div>
            <div class="stat-label">Expert Chefs</div>
          </div>
          <div class="stat-divider"></div>
          <div class="stat">
            <div class="stat-number">2000+</div>
            <div class="stat-label">Happy Customers</div>
          </div>
        </div>
      </div>

      <div class="hero-visual">
        <div class="visual-container">
          <!-- Central intertwining ribbon (Teal) -->
          <div class="ribbon-container">
            <div class="ribbon ribbon-left"></div>
            <div class="ribbon ribbon-right"></div>
            <div class="ribbon ribbon-center"></div>
          </div>

          <!-- Decorative elements with color scheme -->
          <div class="fork-icon">
            <svg width="40" height="40" viewBox="0 0 24 24" fill="none" stroke="#FF5722" stroke-width="2">
              <path d="M5 2v7c0 2.21 1.79 4 4 4s4-1.79 4-4V2M9 13v9M15 2v3c0 1.66-1.34 3-3 3" />
              <path d="M19 2v5c0 1.66-1.34 3-3 3" />
            </svg>
          </div>

          <div class="spoon-icon">
            <svg width="40" height="40" viewBox="0 0 24 24" fill="none" stroke="#2ECC71" stroke-width="2">
              <path d="M12 2v11M8 9c0-2.21 1.79-4 4-4s4 1.79 4 4" />
              <path d="M8 13h8" />
            </svg>
          </div>

          <!-- Stars (Cyan) -->
          <div class="stars">
            <div class="star star-1">⭐</div>
            <div class="star star-2">⭐</div>
            <div class="star star-3">⭐</div>
            <div class="star star-4">⭐</div>
            <div class="star star-5">⭐</div>
          </div>

          <!-- Flame accent -->
          <div class="flame"></div>

          <!-- Leaf accent -->
          <div class="leaf"></div>

          <!-- Left Loop -->
          <div class="left-loop"></div>

          <!-- Right Loop -->
          <div class="right-loop"></div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'HeroSection'
}
</script>

<style scoped>
.hero {
  background: linear-gradient(135deg, #fff8f5 0%, #f0faf2 100%);
  min-height: calc(100vh - 80px);
  display: flex;
  align-items: center;
  overflow: hidden;
  position: relative;
}

.hero-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 4rem 2rem;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
}

.hero-badge {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  background: rgba(255, 87, 34, 0.1);
  padding: 0.5rem 1rem;
  border-radius: 50px;
  margin-bottom: 1.5rem;
}

.badge-dot {
  width: 8px;
  height: 8px;
  background: #FF5722;
  border-radius: 50%;
  animation: pulse 2s infinite;
}

.badge-text {
  color: #FF5722;
  font-weight: 500;
  font-size: 0.875rem;
}

@keyframes pulse {
  0%, 100% { opacity: 1; transform: scale(1); }
  50% { opacity: 0.5; transform: scale(1.2); }
}

.hero-title {
  font-size: 3.5rem;
  font-weight: 800;
  line-height: 1.2;
  margin-bottom: 1.5rem;
  color: #1a1a1a;
}

.orange-text {
  color: #FF5722;
  position: relative;
  display: inline-block;
}

.orange-text::before {
  content: '';
  position: absolute;
  bottom: 5px;
  left: 0;
  width: 100%;
  height: 8px;
  background: rgba(255, 87, 34, 0.2);
  z-index: -1;
}

.green-text {
  color: #2ECC71;
  position: relative;
  display: inline-block;
}

.green-text::before {
  content: '';
  position: absolute;
  bottom: 5px;
  left: 0;
  width: 100%;
  height: 8px;
  background: rgba(46, 204, 113, 0.2);
  z-index: -1;
}

.hero-description {
  font-size: 1.125rem;
  color: #555;
  line-height: 1.6;
  margin-bottom: 2rem;
  max-width: 500px;
}

.hero-buttons {
  display: flex;
  gap: 1rem;
  margin-bottom: 3rem;
}

.btn-orange, .btn-green {
  padding: 0.875rem 2rem;
  border-radius: 50px;
  font-weight: 600;
  font-size: 1rem;
  cursor: pointer;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.btn-orange {
  background: #FF5722;
  border: none;
  color: white;
  box-shadow: 0 5px 15px rgba(255, 87, 34, 0.3);
}

.btn-orange:hover {
  transform: translateY(-3px);
  box-shadow: 0 8px 25px rgba(255, 87, 34, 0.4);
}

.btn-green {
  background: transparent;
  border: 2px solid #2ECC71;
  color: #2ECC71;
}

.btn-green:hover {
  background: #2ECC71;
  color: white;
  transform: translateY(-3px);
}

.btn-icon {
  font-size: 1.125rem;
}

.hero-stats {
  display: flex;
  gap: 2rem;
  align-items: center;
}

.stat {
  text-align: center;
}

.stat-number {
  font-size: 1.75rem;
  font-weight: 800;
  color: #006A7C;
}

.stat-label {
  font-size: 0.875rem;
  color: #666;
}

.stat-divider {
  width: 1px;
  height: 30px;
  background: #ddd;
}

/* Visual Container Styling */
.hero-visual {
  position: relative;
  height: 450px;
}

.visual-container {
  position: relative;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

/* Central Intertwining Ribbon (Teal / Deep Blue) */
.ribbon-container {
  position: relative;
  width: 300px;
  height: 300px;
}

.ribbon {
  position: absolute;
  border-radius: 40% 60% 70% 30% / 40% 50% 60% 50%;
  animation: float 6s ease-in-out infinite;
}

.ribbon-left {
  width: 180px;
  height: 180px;
  background: rgba(0, 106, 124, 0.15);
  border: 3px solid #006A7C;
  top: 60px;
  left: 20px;
  animation-delay: 0s;
}

.ribbon-right {
  width: 180px;
  height: 180px;
  background: rgba(0, 106, 124, 0.1);
  border: 2px solid #006A7C;
  bottom: 60px;
  right: 20px;
  animation-delay: 0.5s;
}

.ribbon-center {
  width: 220px;
  height: 220px;
  background: linear-gradient(135deg, rgba(0,106,124,0.08), rgba(0,106,124,0.02));
  border: 2px dashed #006A7C;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  animation-delay: 0.3s;
}

@keyframes float {
  0%, 100% { transform: translateY(0px) rotate(0deg); }
  50% { transform: translateY(-15px) rotate(5deg); }
}

/* Fork Icon */
.fork-icon {
  position: absolute;
  top: 20px;
  left: -10px;
  animation: bounce 2s ease-in-out infinite;
}

/* Spoon Icon */
.spoon-icon {
  position: absolute;
  bottom: 20px;
  right: -10px;
  animation: bounce 2s ease-in-out infinite 0.5s;
}

@keyframes bounce {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-10px); }
}

/* Stars (Cyan) */
.stars {
  position: absolute;
  width: 100%;
  height: 100%;
}

.star {
  position: absolute;
  font-size: 1.25rem;
  animation: twinkle 2s ease-in-out infinite;
  color: #3FC1D0;
}

.star-1 { top: 20px; right: 40px; animation-delay: 0s; font-size: 1.5rem; }
.star-2 { top: 120px; right: 10px; animation-delay: 0.3s; font-size: 1rem; }
.star-3 { bottom: 100px; left: 30px; animation-delay: 0.6s; font-size: 1.25rem; }
.star-4 { top: 200px; left: -15px; animation-delay: 0.9s; font-size: 1.125rem; }
.star-5 { bottom: 40px; right: 60px; animation-delay: 0.2s; font-size: 1.375rem; }

@keyframes twinkle {
  0%, 100% { opacity: 1; transform: scale(1); }
  50% { opacity: 0.3; transform: scale(0.8); }
}

/* Flame */
.flame {
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 60px;
  height: 80px;
  background: linear-gradient(135deg, #FF5722, #ff784e);
  border-radius: 50% 50% 50% 50% / 60% 60% 40% 40%;
  filter: blur(8px);
  opacity: 0.6;
  animation: flicker 1s ease-in-out infinite;
}

@keyframes flicker {
  0%, 100% { transform: translateX(-50%) scale(1); opacity: 0.6; }
  50% { transform: translateX(-50%) scale(1.1); opacity: 0.8; }
}

/* Leaf */
.leaf {
  position: absolute;
  top: 20px;
  right: 60px;
  width: 40px;
  height: 40px;
  background: #2ECC71;
  border-radius: 80% 0 80% 0;
  transform: rotate(45deg);
  opacity: 0.5;
  animation: leafFloat 3s ease-in-out infinite;
}

@keyframes leafFloat {
  0%, 100% { transform: rotate(45deg) translateY(0); }
  50% { transform: rotate(45deg) translateY(-10px); }
}

/* Left Loop */
.left-loop {
  position: absolute;
  top: 80px;
  left: -20px;
  width: 80px;
  height: 80px;
  border: 3px solid #FF5722;
  border-radius: 40% 60% 70% 30% / 40% 50% 60% 50%;
  opacity: 0.4;
  animation: spinLoop 8s linear infinite;
}

/* Right Loop */
.right-loop {
  position: absolute;
  bottom: 60px;
  right: -30px;
  width: 100px;
  height: 100px;
  border: 3px solid #2ECC71;
  border-radius: 60% 40% 30% 70% / 60% 30% 70% 40%;
  opacity: 0.4;
  animation: spinLoop 8s linear infinite reverse;
}

@keyframes spinLoop {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}

@media (max-width: 968px) {
  .hero-container {
    grid-template-columns: 1fr;
    gap: 2rem;
    text-align: center;
  }

  .hero-description {
    margin-left: auto;
    margin-right: auto;
  }

  .hero-buttons {
    justify-content: center;
  }

  .hero-stats {
    justify-content: center;
  }

  .hero-title {
    font-size: 2.5rem;
  }

  .hero-visual {
    height: 350px;
  }
}
</style>