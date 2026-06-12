<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

// Initialize to true so the overlay is present instantly on page load
const showIntro = ref(true);
const isDarkNav = ref(false);

const handleNavToggle = (e) => {
  isDarkNav.value = e.detail;
};

onMounted(() => {
  // Listen for dark sections covering the screen
  window.addEventListener('toggle-nav-dark', handleNavToggle);

  // Hide overlay after animation sequence completes (3.2 seconds)
  setTimeout(() => {
    showIntro.value = false;
  }, 3200);
});

onUnmounted(() => {
  window.removeEventListener('toggle-nav-dark', handleNavToggle);
});
</script>

<template>
  <div class="app-container">
    
    <!-- Premium Crane Loading Animation -->
    <Transition name="slide-up">
      <div v-if="showIntro" class="intro-overlay">
        
        <div class="intro-content">
          <div class="crane-container">
            <!-- The wire that drops down from the top of the screen -->
            <div class="crane-line"></div>
            <!-- The Logo Payload -->
            <div class="payload">
              <img src="/images/Logo.png" alt="AC Construction" class="intro-logo" />
            </div>
          </div>
          
          <div class="intro-text">
            <span class="text-mask"><span class="line-1">Engineering the</span></span>
            <span class="text-mask"><span class="line-2">Marshall Islands</span></span>
            <span class="text-mask"><span class="line-3 since-text">Since 1989</span></span>
          </div>
        </div>
      </div>
    </Transition>

    <header class="navbar">
      <div class="logo">
        <router-link to="/" style="display: flex; align-items: center;">
          <img src="/images/Logo.png" alt="AC Construction" class="main-logo" :class="{ 'invert-logo': isDarkNav }" />
        </router-link>
      </div>
      <nav class="nav-links">
        <router-link to="/">Home</router-link>
        <router-link to="/about">About Us</router-link>
        <router-link to="/services">Services</router-link>
        <router-link to="/contact">Contact</router-link>
      </nav>
      <div class="navbar-action">
        <router-link to="/contact" custom v-slot="{ navigate }">
          <button @click="navigate" class="btn-primary">Book a meeting</button>
        </router-link>
      </div>
    </header>

    <main>
      <router-view />
    </main>
  </div>
</template>

<style scoped>
.main-logo {
  height: 32px;
  width: auto;
  transition: filter 0.4s ease;
}
.invert-logo {
  filter: invert(1) brightness(200%);
}

/* Intro Overlay Styles */
.intro-overlay {
  position: fixed;
  top: 0; left: 0; right: 0; bottom: 0;
  background-color: #fff;
  z-index: 99999;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.intro-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 40px;
}

/* Crane Animation */
.crane-container {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  /* Drops down from off-screen */
  animation: dropPayload 1.2s cubic-bezier(0.2, 0.8, 0.2, 1) forwards;
}

.crane-line {
  position: absolute;
  bottom: 100%;
  left: 50%;
  transform: translateX(-50%);
  width: 2px;
  height: 100vh;
  background-color: #111;
  /* Wire retracts back up at 2.2s */
  animation: retractWire 0.6s cubic-bezier(0.5, 0, 0.1, 1) 2.2s forwards;
}

.payload {
  padding-top: 10px;
  position: relative;
}

/* The horizontal bar simulating the crane hook */
.payload::before {
  content: '';
  position: absolute;
  top: 0; left: 50%;
  transform: translateX(-50%);
  width: 40px;
  height: 4px;
  background-color: #111;
  border-radius: 4px;
  /* Hook disappears when wire retracts */
  animation: fadeOut 0.2s linear 2.2s forwards;
}

.intro-logo {
  height: 60px;
  width: auto;
  margin-top: 12px;
}

/* Text Reveal Animation */
.intro-text {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
}

.text-mask {
  overflow: hidden;
  display: inline-block;
}

.text-mask span {
  display: inline-block;
  font-size: 13px;
  letter-spacing: 8px;
  text-transform: uppercase;
  font-weight: 500;
  transform: translateY(110%);
}

.line-1 {
  color: #888;
  animation: revealText 0.8s cubic-bezier(0.16, 1, 0.3, 1) 1.0s forwards;
}

.line-2 {
  color: #111;
  animation: revealText 0.8s cubic-bezier(0.16, 1, 0.3, 1) 1.2s forwards;
}

.line-3.since-text {
  color: #666;
  font-size: 11px;
  letter-spacing: 4px;
  margin-top: 8px;
  animation: revealText 0.8s cubic-bezier(0.16, 1, 0.3, 1) 1.4s forwards;
}

/* Keyframes */
@keyframes dropPayload {
  0% { transform: translateY(-60vh); }
  100% { transform: translateY(0); }
}

@keyframes retractWire {
  0% { height: 100vh; }
  100% { height: 0; opacity: 0; }
}

@keyframes revealText {
  0% { transform: translateY(110%); }
  100% { transform: translateY(0); }
}

@keyframes fadeOut {
  0% { opacity: 1; }
  100% { opacity: 0; }
}

/* Outro Transition: Straight Slide Up */
.slide-up-leave-active {
  transition: transform 0.9s cubic-bezier(0.7, 0, 0.2, 1);
}

.slide-up-leave-to {
  transform: translateY(-100%);
}
</style>
