<!-- components/Navbar.vue -->
<template>
  <nav class="navbar">
    <div class="navbar-container">
      <!-- Logo Area - Using your provided image -->
      <div class="logo-area">
        <img :src="logoImage" alt="Food Fusion Logo" class="logo-img" />
      </div>

      <!-- Desktop Navigation -->
      <div class="nav-links-desktop">
        <a
            v-for="item in navItems"
            :key="item.name"
            href="#"
            class="nav-item"
            :class="{ active: activeNav === item.name }"
            @click.prevent="activeNav = item.name"
        >
          {{ item.name }}
          <span class="nav-indicator"></span>
        </a>
      </div>

      <!-- Right Side Actions -->
      <div class="actions-area">
        <!-- Search -->
        <div class="search-container">
          <button class="action-btn search-trigger" @click="toggleSearch">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <circle cx="11" cy="11" r="8"/>
              <path d="M21 21L16.65 16.65"/>
            </svg>
          </button>
          <transition name="search-slide">
            <div v-if="isSearchOpen" class="search-expanded">
              <input
                  type="text"
                  placeholder="Search for dishes..."
                  v-model="searchQuery"
                  ref="searchInput"
              />
              <button @click="isSearchOpen = false" class="search-close">✕</button>
            </div>
          </transition>
        </div>

        <!-- Cart -->
        <div class="cart-container">
          <button class="action-btn cart-btn" @click="toggleCart">
            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <path d="M6 2L3 6v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2V6l-3-4z"/>
              <line x1="3" y1="6" x2="21" y2="6"/>
              <path d="M16 10a4 4 0 0 1-8 0"/>
            </svg>
            <span class="cart-count" v-if="cartTotal > 0">{{ cartTotal }}</span>
          </button>

          <transition name="cart-popup">
            <div v-if="isCartOpen" class="cart-dropdown">
              <div class="cart-header">
                <h4>Your Cart</h4>
                <button class="cart-close" @click="isCartOpen = false">✕</button>
              </div>
              <div class="cart-items" v-if="cartItems.length">
                <div v-for="item in cartItems" :key="item.id" class="cart-item">
                  <div class="cart-item-img" :style="{ backgroundImage: `url(${item.image})` }"></div>
                  <div class="cart-item-details">
                    <p class="cart-item-name">{{ item.name }}</p>
                    <p class="cart-item-price">${{ item.price }}</p>
                  </div>
                  <button class="cart-remove-btn">✕</button>
                </div>
              </div>
              <div class="cart-empty" v-else>
                <svg width="48" height="48" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
                  <path d="M6 2L3 6v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2V6l-3-4z"/>
                  <line x1="3" y1="6" x2="21" y2="6"/>
                  <path d="M16 10a4 4 0 0 1-8 0"/>
                </svg>
                <p>Your cart is empty</p>
              </div>
              <div class="cart-footer" v-if="cartItems.length">
                <div class="cart-total">
                  <span>Total</span>
                  <span>${{ cartTotalAmount }}</span>
                </div>
                <button class="checkout-btn">Checkout →</button>
              </div>
            </div>
          </transition>
        </div>

        <!-- User -->
        <div class="user-container">
          <button class="user-btn" @click="toggleUserMenu">
            <div class="user-avatar">
              <span>{{ userInitial }}</span>
            </div>
            <svg class="dropdown-arrow" :class="{ rotated: isUserMenuOpen }" width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <polyline points="6 9 12 15 18 9"/>
            </svg>
          </button>

          <transition name="dropdown-fade">
            <div v-if="isUserMenuOpen" class="user-dropdown">
              <div class="user-info">
                <div class="dropdown-avatar">{{ userInitial }}</div>
                <div>
                  <p class="user-name-dropdown">{{ userName }}</p>
                  <p class="user-email-dropdown">{{ userEmail }}</p>
                </div>
              </div>
              <div class="dropdown-divider"></div>
              <a href="#" class="dropdown-link">
                <span class="dropdown-icon">👤</span>
                Profile
              </a>
              <a href="#" class="dropdown-link">
                <span class="dropdown-icon">📦</span>
                Orders
              </a>
              <a href="#" class="dropdown-link">
                <span class="dropdown-icon">❤️</span>
                Favorites
              </a>
              <a href="#" class="dropdown-link">
                <span class="dropdown-icon">⚙️</span>
                Settings
              </a>
              <div class="dropdown-divider"></div>
              <a href="#" class="dropdown-link logout">
                <span class="dropdown-icon">🚪</span>
                Sign Out
              </a>
            </div>
          </transition>
        </div>

        <!-- CTA Button -->
        <button class="cta-button">
          <span>Reserve Now</span>
          <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M5 12h14M12 5l7 7-7 7"/>
          </svg>
        </button>
      </div>

      <!-- Mobile Menu Button -->
      <button class="mobile-menu-btn" @click="toggleMobileMenu" :class="{ active: isMobileMenuOpen }">
        <span></span>
        <span></span>
        <span></span>
      </button>
    </div>

    <!-- Mobile Navigation -->
    <transition name="mobile-slide">
      <div v-if="isMobileMenuOpen" class="mobile-menu">
        <div class="mobile-menu-header">
          <img :src="logoImage" alt="Logo" class="mobile-logo-img" />
          <button class="mobile-close" @click="toggleMobileMenu">✕</button>
        </div>

        <div class="mobile-nav-links">
          <a
              v-for="item in navItems"
              :key="item.name"
              href="#"
              class="mobile-nav-link"
              :class="{ active: activeNav === item.name }"
              @click.prevent="activeNav = item.name; toggleMobileMenu()"
          >
            {{ item.name }}
          </a>
        </div>

        <div class="mobile-actions">
          <div class="mobile-search">
            <input type="text" placeholder="Search for dishes..." />
            <button>🔍</button>
          </div>
          <button class="mobile-cta">Reserve a Table →</button>
        </div>
      </div>
    </transition>

    <!-- Backdrop -->
    <transition name="fade">
      <div v-if="isMobileMenuOpen" class="mobile-backdrop" @click="toggleMobileMenu"></div>
    </transition>
  </nav>
</template>

<script>
import logoImage from '@/assets/foodfusion.png'

export default {
  name: 'Navbar',
  data() {
    return {
      logoImage: logoImage,
      navItems: [
        { name: 'Home', path: '/' },
        { name: 'Menu', path: '/menu' },
        { name: 'About', path: '/about' },
        { name: 'Contact', path: '/contact' }
      ],
      activeNav: 'Home',
      isMobileMenuOpen: false,
      isUserMenuOpen: false,
      isCartOpen: false,
      isSearchOpen: false,
      searchQuery: '',
      userName: 'Emma Watson',
      userEmail: 'emma@foodfusion.com',
      userInitial: 'E',
      cartTotal: 3,
      cartItems: [
        { id: 1, name: 'Truffle Pasta', price: '24.99', image: '' },
        { id: 2, name: 'Margherita Pizza', price: '18.99', image: '' },
        { id: 3, name: 'Tiramisu', price: '8.99', image: '' }
      ]
    }
  },
  computed: {
    cartTotalAmount() {
      return this.cartItems.reduce((sum, item) => sum + parseFloat(item.price), 0).toFixed(2)
    }
  },
  methods: {
    toggleMobileMenu() {
      this.isMobileMenuOpen = !this.isMobileMenuOpen
      if (this.isMobileMenuOpen) {
        document.body.style.overflow = 'hidden'
      } else {
        document.body.style.overflow = ''
      }
    },
    toggleUserMenu() {
      this.isUserMenuOpen = !this.isUserMenuOpen
      if (this.isUserMenuOpen) {
        this.isCartOpen = false
      }
    },
    toggleCart() {
      this.isCartOpen = !this.isCartOpen
      if (this.isCartOpen) {
        this.isUserMenuOpen = false
      }
    },
    toggleSearch() {
      this.isSearchOpen = !this.isSearchOpen
      if (this.isSearchOpen) {
        this.$nextTick(() => {
          this.$refs.searchInput?.focus()
        })
      }
    }
  },
  mounted() {
    document.addEventListener('click', (e) => {
      if (!e.target.closest('.user-container')) this.isUserMenuOpen = false
      if (!e.target.closest('.cart-container')) this.isCartOpen = false
      if (!e.target.closest('.search-container')) this.isSearchOpen = false
    })
  },
  beforeUnmount() {
    document.body.style.overflow = ''
  }
}
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  background: rgba(255, 255, 255, 0.96);
  backdrop-filter: blur(12px);
  border-bottom: 1px solid rgba(0, 0, 0, 0.06);
  transition: all 0.3s ease;
}

.navbar-container {
  max-width: 1400px;
  margin: 0 auto;
  padding: 0.9rem 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

/* Logo Area */
.logo-area {
  flex-shrink: 0;
  cursor: pointer;
  transition: transform 0.3s cubic-bezier(0.2, 0.9, 0.4, 1.1);
}

.logo-area:hover {
  transform: scale(1.02);
}

.logo-img {
  height: 48px;
  width: auto;
  object-fit: contain;
  transition: all 0.3s ease;
}

/* Desktop Navigation */
.nav-links-desktop {
  display: flex;
  gap: 0.5rem;
  align-items: center;
  background: rgba(0, 0, 0, 0.02);
  padding: 0.25rem;
  border-radius: 50px;
}

.nav-item {
  position: relative;
  color: #5a5a6e;
  text-decoration: none;
  font-weight: 500;
  font-size: 0.95rem;
  padding: 0.6rem 1.2rem;
  border-radius: 40px;
  transition: all 0.3s cubic-bezier(0.2, 0.9, 0.4, 1.1);
}

.nav-item:hover {
  color: #1a1a2e;
  background: rgba(0, 0, 0, 0.04);
}

.nav-indicator {
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%) scaleX(0);
  width: 30px;
  height: 3px;
  background: linear-gradient(90deg, #FF6B35, #FF8C5A);
  border-radius: 3px;
  transition: transform 0.3s cubic-bezier(0.2, 0.9, 0.4, 1.1);
}

.nav-item:hover .nav-indicator,
.nav-item.active .nav-indicator {
  transform: translateX(-50%) scaleX(1);
}

.nav-item.active {
  color: #1a1a2e;
  background: rgba(0, 0, 0, 0.03);
}

/* Actions Area */
.actions-area {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.action-btn {
  background: transparent;
  border: none;
  padding: 0.5rem;
  cursor: pointer;
  color: #6b6b80;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.3s cubic-bezier(0.2, 0.9, 0.4, 1.1);
}

.action-btn:hover {
  color: #FF6B35;
  background: rgba(255, 107, 53, 0.1);
  transform: translateY(-2px);
}

/* Search */
.search-container {
  position: relative;
}

.search-expanded {
  position: absolute;
  top: 50%;
  right: 45px;
  transform: translateY(-50%);
  display: flex;
  align-items: center;
  gap: 0.5rem;
  background: white;
  border-radius: 50px;
  padding: 0.25rem 0.25rem 0.25rem 1rem;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
  border: 1px solid rgba(0, 0, 0, 0.08);
}

.search-expanded input {
  background: transparent;
  border: none;
  padding: 0.6rem 0;
  color: #1a1a2e;
  font-size: 0.85rem;
  width: 220px;
  outline: none;
}

.search-expanded input::placeholder {
  color: #aaa;
}

.search-expanded .search-close {
  background: rgba(0, 0, 0, 0.05);
  border: none;
  color: #6b6b80;
  width: 30px;
  height: 30px;
  border-radius: 50%;
  cursor: pointer;
  font-size: 12px;
  transition: all 0.2s ease;
}

.search-expanded .search-close:hover {
  background: rgba(0, 0, 0, 0.1);
  color: #1a1a2e;
}

.search-slide-enter-active, .search-slide-leave-active {
  transition: all 0.25s cubic-bezier(0.2, 0.9, 0.4, 1.1);
}

.search-slide-enter-from, .search-slide-leave-to {
  opacity: 0;
  transform: translateX(20px) translateY(-50%);
}

/* Cart */
.cart-container {
  position: relative;
}

.cart-btn {
  position: relative;
}

.cart-count {
  position: absolute;
  top: -4px;
  right: -4px;
  background: linear-gradient(135deg, #FF6B35, #FF8C5A);
  color: white;
  font-size: 0.6rem;
  font-weight: 600;
  padding: 0.1rem 0.35rem;
  border-radius: 20px;
  min-width: 18px;
  height: 18px;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 2px 6px rgba(255, 107, 53, 0.3);
}

.cart-dropdown {
  position: absolute;
  top: 48px;
  right: -10px;
  width: 340px;
  background: white;
  border-radius: 20px;
  box-shadow: 0 15px 40px rgba(0, 0, 0, 0.1);
  border: 1px solid rgba(0, 0, 0, 0.06);
  overflow: hidden;
  z-index: 100;
}

.cart-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 1.25rem;
  border-bottom: 1px solid #f0f0f0;
}

.cart-header h4 {
  color: #1a1a2e;
  font-size: 1rem;
  font-weight: 600;
}

.cart-close {
  background: transparent;
  border: none;
  color: #aaa;
  cursor: pointer;
  font-size: 16px;
  transition: color 0.2s ease;
}

.cart-close:hover {
  color: #1a1a2e;
}

.cart-items {
  max-height: 320px;
  overflow-y: auto;
}

.cart-item {
  display: flex;
  gap: 1rem;
  padding: 0.85rem 1.25rem;
  border-bottom: 1px solid #f5f5f5;
  transition: background 0.2s ease;
}

.cart-item:hover {
  background: #fafafa;
}

.cart-item-img {
  width: 52px;
  height: 52px;
  background: linear-gradient(135deg, #FF6B35, #FF8C5A);
  border-radius: 12px;
  flex-shrink: 0;
}

.cart-item-details {
  flex: 1;
}

.cart-item-name {
  color: #1a1a2e;
  font-size: 0.9rem;
  font-weight: 500;
  margin-bottom: 4px;
}

.cart-item-price {
  color: #FF6B35;
  font-size: 0.85rem;
  font-weight: 600;
}

.cart-remove-btn {
  background: transparent;
  border: none;
  color: #ccc;
  cursor: pointer;
  font-size: 12px;
  transition: color 0.2s ease;
}

.cart-remove-btn:hover {
  color: #e74c3c;
}

.cart-empty {
  padding: 2rem;
  text-align: center;
}

.cart-empty svg {
  stroke: #ddd;
  margin-bottom: 1rem;
}

.cart-empty p {
  color: #999;
  font-size: 0.85rem;
}

.cart-footer {
  padding: 1rem 1.25rem;
  border-top: 1px solid #f0f0f0;
  background: #fefefe;
}

.cart-total {
  display: flex;
  justify-content: space-between;
  color: #1a1a2e;
  font-weight: 600;
  margin-bottom: 1rem;
}

.checkout-btn {
  width: 100%;
  padding: 0.75rem;
  background: linear-gradient(135deg, #FF6B35, #FF8C5A);
  border: none;
  border-radius: 40px;
  color: white;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
}

.checkout-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(255, 107, 53, 0.3);
}

/* User Menu */
.user-container {
  position: relative;
}

.user-btn {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  background: transparent;
  border: none;
  cursor: pointer;
  padding: 0.2rem 0.5rem 0.2rem 0.2rem;
  border-radius: 40px;
  transition: all 0.3s ease;
}

.user-btn:hover {
  background: rgba(0, 0, 0, 0.04);
}

.user-avatar {
  width: 36px;
  height: 36px;
  background: linear-gradient(135deg, #FF6B35, #FF8C5A);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-weight: 600;
  font-size: 0.9rem;
  transition: transform 0.3s ease;
}

.user-btn:hover .user-avatar {
  transform: scale(1.05);
}

.dropdown-arrow {
  color: #aaa;
  transition: transform 0.3s ease;
}

.dropdown-arrow.rotated {
  transform: rotate(180deg);
}

.user-dropdown {
  position: absolute;
  top: 48px;
  right: 0;
  width: 260px;
  background: white;
  border-radius: 20px;
  box-shadow: 0 15px 40px rgba(0, 0, 0, 0.1);
  border: 1px solid rgba(0, 0, 0, 0.06);
  overflow: hidden;
  z-index: 100;
}

.user-info {
  display: flex;
  gap: 1rem;
  padding: 1.2rem;
  background: #fefefe;
  border-bottom: 1px solid #f0f0f0;
}

.dropdown-avatar {
  width: 44px;
  height: 44px;
  background: linear-gradient(135deg, #FF6B35, #FF8C5A);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-weight: 600;
  font-size: 1rem;
}

.user-name-dropdown {
  color: #1a1a2e;
  font-weight: 600;
  font-size: 0.9rem;
}

.user-email-dropdown {
  color: #999;
  font-size: 0.7rem;
  margin-top: 2px;
}

.dropdown-divider {
  height: 1px;
  background: #f0f0f0;
  margin: 0.25rem 0;
}

.dropdown-link {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 0.75rem 1.2rem;
  color: #5a5a6e;
  text-decoration: none;
  font-size: 0.85rem;
  transition: all 0.25s ease;
}

.dropdown-link:hover {
  background: rgba(255, 107, 53, 0.06);
  color: #FF6B35;
  padding-left: 1.5rem;
}

.dropdown-icon {
  font-size: 1rem;
  width: 24px;
}

.dropdown-link.logout {
  color: #e74c3c;
}

.dropdown-link.logout:hover {
  background: rgba(231, 76, 60, 0.06);
  color: #e74c3c;
}

/* CTA Button */
.cta-button {
  background: linear-gradient(135deg, #FF6B35, #FF8C5A);
  border: none;
  padding: 0.6rem 1.25rem;
  border-radius: 40px;
  color: white;
  font-weight: 600;
  font-size: 0.85rem;
  cursor: pointer;
  display: flex;
  align-items: center;
  gap: 0.5rem;
  transition: all 0.3s cubic-bezier(0.2, 0.9, 0.4, 1.1);
  box-shadow: 0 2px 8px rgba(255, 107, 53, 0.2);
}

.cta-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 16px rgba(255, 107, 53, 0.3);
}

.cta-button svg {
  transition: transform 0.3s ease;
}

.cta-button:hover svg {
  transform: translateX(4px);
}

/* Mobile Menu Button */
.mobile-menu-btn {
  display: none;
  flex-direction: column;
  gap: 5px;
  background: transparent;
  border: none;
  cursor: pointer;
  padding: 0.5rem;
}

.mobile-menu-btn span {
  width: 24px;
  height: 2px;
  background: #1a1a2e;
  border-radius: 2px;
  transition: all 0.3s ease;
}

.mobile-menu-btn.active span:nth-child(1) {
  transform: rotate(45deg) translate(5px, 5px);
}

.mobile-menu-btn.active span:nth-child(2) {
  opacity: 0;
}

.mobile-menu-btn.active span:nth-child(3) {
  transform: rotate(-45deg) translate(5px, -5px);
}

/* Mobile Menu */
.mobile-menu {
  position: fixed;
  top: 0;
  right: 0;
  width: 85%;
  max-width: 340px;
  height: 100vh;
  background: white;
  z-index: 1002;
  padding: 1.5rem;
  display: flex;
  flex-direction: column;
  gap: 2rem;
  box-shadow: -5px 0 30px rgba(0, 0, 0, 0.1);
}

.mobile-menu-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.mobile-logo-img {
  height: 44px;
  width: auto;
}

.mobile-close {
  background: rgba(0, 0, 0, 0.05);
  border: none;
  color: #6b6b80;
  width: 36px;
  height: 36px;
  border-radius: 50%;
  cursor: pointer;
  font-size: 16px;
  transition: all 0.2s ease;
}

.mobile-close:hover {
  background: rgba(0, 0, 0, 0.1);
  color: #1a1a2e;
}

.mobile-nav-links {
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
}

.mobile-nav-link {
  color: #5a5a6e;
  text-decoration: none;
  font-size: 1.1rem;
  font-weight: 500;
  padding: 0.9rem 0;
  border-bottom: 1px solid #f0f0f0;
  transition: all 0.3s ease;
}

.mobile-nav-link:hover,
.mobile-nav-link.active {
  color: #FF6B35;
  padding-left: 0.75rem;
}

.mobile-actions {
  margin-top: auto;
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.mobile-search {
  display: flex;
  gap: 0.5rem;
}

.mobile-search input {
  flex: 1;
  background: #f5f5f5;
  border: 1px solid #e8e8e8;
  border-radius: 40px;
  padding: 0.8rem 1rem;
  color: #1a1a2e;
  font-size: 0.85rem;
  outline: none;
  transition: all 0.2s ease;
}

.mobile-search input:focus {
  border-color: #FF6B35;
  background: white;
}

.mobile-search input::placeholder {
  color: #aaa;
}

.mobile-search button {
  background: #f5f5f5;
  border: 1px solid #e8e8e8;
  border-radius: 40px;
  padding: 0.8rem 1rem;
  color: #6b6b80;
  cursor: pointer;
  transition: all 0.2s ease;
}

.mobile-search button:hover {
  background: #FF6B35;
  color: white;
  border-color: #FF6B35;
}

.mobile-cta {
  background: linear-gradient(135deg, #FF6B35, #FF8C5A);
  border: none;
  padding: 1rem;
  border-radius: 40px;
  color: white;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
}

.mobile-cta:hover {
  transform: translateY(-2px);
}

.mobile-backdrop {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.4);
  backdrop-filter: blur(4px);
  z-index: 1001;
}

/* Transitions */
.cart-popup-enter-active, .cart-popup-leave-active,
.dropdown-fade-enter-active, .dropdown-fade-leave-active {
  transition: all 0.2s cubic-bezier(0.2, 0.9, 0.4, 1.1);
}

.cart-popup-enter-from, .cart-popup-leave-to,
.dropdown-fade-enter-from, .dropdown-fade-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}

.mobile-slide-enter-active, .mobile-slide-leave-active {
  transition: transform 0.3s cubic-bezier(0.2, 0.9, 0.4, 1.1);
}

.mobile-slide-enter-from, .mobile-slide-leave-to {
  transform: translateX(100%);
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.25s ease;
}

.fade-enter-from, .fade-leave-to {
  opacity: 0;
}

/* Responsive */
@media (max-width: 968px) {
  .nav-links-desktop {
    display: none;
  }

  .mobile-menu-btn {
    display: flex;
  }

  .navbar-container {
    padding: 0.8rem 1.5rem;
  }

  .cta-button {
    display: none;
  }
}

@media (max-width: 640px) {
  .actions-area {
    gap: 0.25rem;
  }

  .cart-dropdown {
    position: fixed;
    top: auto;
    bottom: 0;
    left: 0;
    right: 0;
    width: 100%;
    border-radius: 20px 20px 0 0;
  }

  .logo-img {
    height: 40px;
  }

  .user-btn .dropdown-arrow {
    display: none;
  }

  .search-expanded {
    position: fixed;
    top: 70px;
    left: 1rem;
    right: 1rem;
    transform: none;
    width: auto;
  }

  .search-expanded input {
    width: 100%;
  }
}
</style>