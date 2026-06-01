<!-- components/Footer.vue -->
<template>
  <footer class="footer">
    <div class="footer-container">
      <div class="footer-brand">
        <div class="brand-logo">
          <img :src="logoImage" alt="Food Fusion Logo" class="footer-logo" />
          <h3>FoodFusion</h3>
        </div>
        <p class="brand-desc">
          Bringing together the world's finest flavors, creating unforgettable dining experiences.
        </p>
        <div class="social-links">
          <a href="#" class="social-link" style="color: #FF5722;">📘</a>
          <a href="#" class="social-link" style="color: #3FC1D0;">🐦</a>
          <a href="#" class="social-link" style="color: #2ECC71;">📷</a>
          <a href="#" class="social-link" style="color: #006A7C;">🔗</a>
        </div>
      </div>

      <div class="footer-links">
        <div class="link-group">
          <h4 class="fork-title">Explore</h4>
          <a href="#">Menu</a>
          <a href="#">Locations</a>
          <a href="#">Catering</a>
          <a href="#">Gift Cards</a>
        </div>

        <div class="link-group">
          <h4 class="green-title">Company</h4>
          <a href="#">About Us</a>
          <a href="#">Careers</a>
          <a href="#">Blog</a>
          <a href="#">Press</a>
        </div>

        <div class="link-group">
          <h4 class="teal-title">Support</h4>
          <a href="#">Contact</a>
          <a href="#">FAQ</a>
          <a href="#">Privacy Policy</a>
          <a href="#">Terms of Service</a>
        </div>

        <div class="link-group newsletter">
          <h4 class="cyan-title">Newsletter</h4>
          <p>Get the latest updates on new dishes and events</p>
          <div class="newsletter-form">
            <input type="email" placeholder="Your email address" />
            <button>→</button>
          </div>
        </div>
      </div>
    </div>

    <div class="footer-bottom">
      <div class="footer-bottom-container">
        <p>&copy; 2024 FoodFusion. All rights reserved.</p>
        <div class="bottom-links">
          <a href="#">Privacy</a>
          <a href="#">Terms</a>
          <a href="#">Sitemap</a>
        </div>
      </div>
    </div>
  </footer>
</template>

<script>
import logoImage from '@/assets/foodfusion.png'

export default {
  name: 'Footer',
  data() {
    return {
      logoImage: logoImage
    }
  }
}
</script>

<style scoped>
.footer {
  background: #1a1a1a;
  color: #ccc;
  margin-top: auto;
}

.footer-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 3rem 2rem;
  display: grid;
  grid-template-columns: 1.5fr 2fr;
  gap: 3rem;
}

.footer-brand {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.brand-logo {
  display: flex;
  align-items: center;
  gap: 0.75rem;
}

.footer-logo {
  height: 40px;
  width: auto;
  object-fit: contain;
}

.brand-logo h3 {
  font-size: 1.5rem;
  background: linear-gradient(135deg, #FF5722, #2ECC71, #006A7C);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
}

.brand-desc {
  line-height: 1.6;
  max-width: 300px;
  font-size: 0.9rem;
}

.social-links {
  display: flex;
  gap: 1rem;
  margin-top: 0.5rem;
}

.social-link {
  width: 36px;
  height: 36px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(255,255,255,0.1);
  border-radius: 50%;
  text-decoration: none;
  font-size: 1.125rem;
  transition: all 0.3s ease;
}

.social-link:hover {
  transform: translateY(-3px);
  background: rgba(255,255,255,0.2);
}

.footer-links {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 2rem;
}

.link-group {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
}

.link-group h4 {
  font-size: 1.1rem;
  font-weight: 600;
  margin-bottom: 0.5rem;
}

.fork-title { color: #FF5722; }
.green-title { color: #2ECC71; }
.teal-title { color: #006A7C; }
.cyan-title { color: #3FC1D0; }

.link-group a {
  color: #aaa;
  text-decoration: none;
  font-size: 0.875rem;
  transition: color 0.3s ease;
}

.link-group a:hover {
  color: white;
}

.newsletter p {
  font-size: 0.8rem;
  color: #888;
}

.newsletter-form {
  display: flex;
  margin-top: 0.5rem;
}

.newsletter-form input {
  flex: 1;
  padding: 0.625rem;
  border: none;
  background: #333;
  color: white;
  border-radius: 25px 0 0 25px;
  outline: none;
}

.newsletter-form button {
  padding: 0.625rem 1rem;
  background: #FF5722;
  border: none;
  color: white;
  border-radius: 0 25px 25px 0;
  cursor: pointer;
  transition: background 0.3s ease;
}

.newsletter-form button:hover {
  background: #e04e1f;
}

.footer-bottom {
  border-top: 1px solid #333;
  padding: 1.5rem 2rem;
}

.footer-bottom-container {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 1rem;
}

.footer-bottom p {
  font-size: 0.8rem;
  color: #888;
}

.bottom-links {
  display: flex;
  gap: 1.5rem;
}

.bottom-links a {
  color: #888;
  text-decoration: none;
  font-size: 0.8rem;
  transition: color 0.3s ease;
}

.bottom-links a:hover {
  color: #FF5722;
}

@media (max-width: 968px) {
  .footer-container {
    grid-template-columns: 1fr;
    gap: 2rem;
  }

  .footer-links {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 576px) {
  .footer-links {
    grid-template-columns: 1fr;
  }

  .footer-bottom-container {
    flex-direction: column;
    text-align: center;
  }
}
</style>