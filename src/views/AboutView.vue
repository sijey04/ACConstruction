<template>
  <div class="about-page">
    <!-- Horizontal Scroll Wrapper -->
    <div class="horizontal-wrapper" ref="scrollWrapper" @wheel="handleWheel">
      
      <!-- Slide 1: Title -->
      <section class="h-slide intro-slide">
        <div class="slide-content">
          <h1 class="huge-title animate-up delay-1">About<br>AC Construction</h1>
          <p class="subtitle animate-up delay-2">Pioneering infrastructural excellence in the Marshall Islands since our founding.</p>
          <div class="scroll-indicator animate-up delay-3">
            <span>Scroll</span>
            <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12h14M12 5l7 7-7 7"/></svg>
          </div>
        </div>
      </section>

      <!-- Slide 2: Heritage -->
      <section class="h-slide content-slide">
        <div class="slide-content split-layout">
          <div class="text-panel animate-up delay-1">
            <span class="label">01 / Heritage</span>
            <h2>Roots in the Marshall Islands</h2>
            <p>
              <strong>AC Construction Co. & Services</strong> operates as a premier subsidiary of Kabkondrikdrik Enterprises Inc. (KEI). 
              Established by the Bing family, our roots run deep in the Marshall Islands. We believe that robust infrastructure is the 
              backbone of a thriving nation. Our mission is to provide world-class construction, earthmoving, and development services 
              while actively prioritizing the creation of sustainable local jobs and empowering our community.
            </p>
          </div>
          <div class="image-panel animate-up delay-2">
            <img src="/images/img1.png" alt="Heritage" />
          </div>
        </div>
      </section>

      <!-- Slide 3: Excellence -->
      <section class="h-slide content-slide">
        <div class="slide-content split-layout">
          <div class="text-panel animate-up delay-1">
            <span class="label">02 / Excellence</span>
            <h2>Commitment to Standards</h2>
            <p>
              From intricate government contracting to large-scale private commercial developments, we approach every project with 
              uncompromising standards. Our operations are driven by a commitment to safety, environmental sustainability, and timely delivery. 
              By combining local expertise with modern engineering practices, we ensure that every structure we build stands the test of time and climate.
            </p>
          </div>
          <div class="image-panel animate-up delay-2">
            <img src="/images/img3.png" alt="Excellence" />
          </div>
        </div>
      </section>

      <!-- Slide 4: Future -->
      <section class="h-slide outro-slide">
        <div class="slide-content center-content">
          <h2 class="animate-up delay-1">Building the future.</h2>
          <div class="animate-up delay-2">
            <router-link to="/contact" class="btn-primary huge-btn">Work With Us</router-link>
          </div>
        </div>
      </section>

    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const scrollWrapper = ref(null);
let darkObserver = null;
let animationObserver = null;

const handleWheel = (e) => {
  // Translate vertical scrolling to horizontal scrolling
  if (scrollWrapper.value) {
    // Check if scrolling up or down
    if (e.deltaY !== 0) {
      e.preventDefault();
      scrollWrapper.value.scrollBy({
        left: e.deltaY * 1.5, // Scroll speed multiplier
        behavior: 'auto'
      });
    }
  }
};

onMounted(() => {
  // Add non-passive event listener for wheel to allow preventDefault
  if (scrollWrapper.value) {
    scrollWrapper.value.addEventListener('wheel', handleWheel, { passive: false });
  }

  // Animation observer
  animationObserver = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('in-view');
      }
    });
  }, { threshold: 0.15 });

  document.querySelectorAll('.animate-up').forEach((el) => {
    animationObserver.observe(el);
  });

  // Observe the dark outro slide to turn the logo white
  const outroSlide = document.querySelector('.outro-slide');
  if (outroSlide) {
    darkObserver = new IntersectionObserver((entries) => {
      window.dispatchEvent(new CustomEvent('toggle-nav-dark', { detail: entries[0].isIntersecting }));
    }, { threshold: 0.5 });
    darkObserver.observe(outroSlide);
  }
});

onUnmounted(() => {
  if (scrollWrapper.value) {
    scrollWrapper.value.removeEventListener('wheel', handleWheel);
  }
  if (darkObserver) {
    darkObserver.disconnect();
  }
  if (animationObserver) {
    animationObserver.disconnect();
  }
  // Reset logo color when leaving the page
  window.dispatchEvent(new CustomEvent('toggle-nav-dark', { detail: false }));
});
</script>

<style scoped>
/* Animations Setup */
.animate-up {
  opacity: 0;
  transform: translateY(40px);
  transition: opacity 0.8s cubic-bezier(0.16, 1, 0.3, 1), transform 0.8s cubic-bezier(0.16, 1, 0.3, 1);
}
.animate-up.in-view {
  opacity: 1;
  transform: translateY(0);
}
.delay-1 { transition-delay: 0.1s; }
.delay-2 { transition-delay: 0.25s; }
.delay-3 { transition-delay: 0.4s; }

.about-page {
  width: 100%;
  height: 100vh;
  background-color: #fff;
  overflow: hidden;
}

.horizontal-wrapper {
  display: flex;
  height: 100%;
  width: 100%;
  overflow-x: auto;
  overflow-y: hidden;
  scroll-snap-type: x mandatory;
  scroll-behavior: smooth;
  /* Hide scrollbar for cleaner look */
  -ms-overflow-style: none;  
  scrollbar-width: none;  
}

.horizontal-wrapper::-webkit-scrollbar {
  display: none;
}

.h-slide {
  flex: 0 0 100vw;
  height: 100%;
  scroll-snap-align: start;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 40px;
}

/* Slide 1 */
.intro-slide {
  background-color: #fcfcfc;
}

.intro-slide .slide-content {
  max-width: 800px;
  text-align: left;
  position: relative;
}

.huge-title {
  font-size: 8vw;
  line-height: 0.9;
  letter-spacing: -0.05em;
  margin-bottom: 32px;
  color: #111;
}

.subtitle {
  font-size: 24px;
  color: #666;
  max-width: 500px;
  line-height: 1.5;
}

.scroll-indicator {
  position: absolute;
  right: -100px;
  bottom: 0;
  display: flex;
  align-items: center;
  gap: 12px;
  color: #111;
  font-weight: 600;
  animation: slideRight 2s infinite;
}

@keyframes slideRight {
  0%, 100% { transform: translateX(0); }
  50% { transform: translateX(10px); }
}

/* Content Slides */
.split-layout {
  display: flex;
  width: 100%;
  max-width: 1400px;
  height: 80vh;
  gap: 80px;
  align-items: center;
}

.text-panel {
  flex: 1;
  padding-right: 40px;
}

.label {
  font-size: 14px;
  text-transform: uppercase;
  letter-spacing: 2px;
  color: #888;
  display: block;
  margin-bottom: 24px;
  font-weight: 600;
}

.text-panel h2 {
  font-size: 48px;
  margin-bottom: 32px;
  letter-spacing: -1px;
  line-height: 1.1;
}

.text-panel p {
  font-size: 18px;
  color: #555;
  line-height: 1.8;
}

.image-panel {
  flex: 1.2;
  height: 100%;
  border-radius: 24px;
  overflow: hidden;
  box-shadow: 0 30px 60px rgba(0,0,0,0.1);
}

.image-panel img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.6s ease;
}

.image-panel:hover img {
  transform: scale(1.05);
}

/* Outro Slide */
.outro-slide {
  background-color: #111;
  color: #fff;
}

.center-content {
  text-align: center;
}

.center-content h2 {
  font-size: 80px;
  margin-bottom: 40px;
  letter-spacing: -2px;
}

.huge-btn {
  font-size: 18px;
  padding: 20px 48px;
  background-color: #fff;
  color: #111;
}

.huge-btn:hover {
  background-color: #f0f0f0;
  transform: scale(1.05);
}

@media (max-width: 1024px) {
  .huge-title { font-size: 6vw; }
  .split-layout { gap: 20px; }
  .text-panel { padding-right: 0; }
  .text-panel h2 { font-size: 32px; margin-bottom: 16px; }
  .text-panel p { font-size: 14px; line-height: 1.5; }
  .subtitle { font-size: 16px; max-width: 80%; }
}

@media (max-width: 768px) {
  .huge-title { font-size: 32px; }
  .split-layout { gap: 10px; align-items: center; justify-content: center; }
  .text-panel h2 { font-size: 20px; margin-bottom: 12px; }
  .text-panel p { font-size: 11px; line-height: 1.4; }
  .label { font-size: 10px; margin-bottom: 8px; }
  .h-slide { padding: 20px; }
  .image-panel { height: 40vh; box-shadow: 0 10px 20px rgba(0,0,0,0.1); }
  .center-content h2 { font-size: 32px; margin-bottom: 24px; }
  .huge-btn { padding: 12px 24px; font-size: 14px; }
  .scroll-indicator { right: 0; bottom: 20px; }
}
</style>
