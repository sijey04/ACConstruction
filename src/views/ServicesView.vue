<template>
  <div class="services-page">
    
    <!-- Intro Slide -->
    <section class="scroll-section services-header">
      <div class="header-content animate-up delay-1">
        <h1 class="huge-title">Our Expertise.</h1>
        <p class="subtitle">Uncompromising standards in civil engineering, marine infrastructure, and bespoke commercial construction.</p>
      </div>
    </section>

    <!-- Service 1 -->
    <section class="scroll-section service-row">
      <div class="service-text animate-up delay-1">
        <span class="service-num">01 / Structural</span>
        <h2>Commercial Construction</h2>
        <p>
          Delivering full-scale structural developments from private high-end complexes to critical public facilities. 
          We integrate modern architectural techniques with climate-resilient engineering tailored specifically 
          for the unique demands of the Marshall Islands.
        </p>
        <ul class="feature-list">
          <li>Private Residences</li>
          <li>Government Facilities</li>
          <li>Healthcare & Education</li>
        </ul>
      </div>
      <div class="service-visual animate-up delay-2">
        <div class="image-wrapper">
          <img src="/images/img4.png" alt="Commercial Construction" />
        </div>
      </div>
    </section>

    <!-- Service 2 -->
    <section class="scroll-section service-row reverse">
      <div class="service-text animate-up delay-1">
        <span class="service-num">02 / Heavy Civil</span>
        <h2>Earthworks & Marine</h2>
        <p>
          Protecting and expanding the nation's most valuable asset: its land. We operate a dedicated fleet 
          of heavy machinery to execute massive earthmoving, coastal reclamation, and robust seawall defenses.
        </p>
        <ul class="feature-list">
          <li>Coastal Reclamation</li>
          <li>Seawall Defenses</li>
          <li>Dredging Operations</li>
        </ul>
      </div>
      <div class="service-visual animate-up delay-2">
        <div class="image-wrapper">
          <img src="/images/img2.png" alt="Earthworks & Marine" />
        </div>
      </div>
    </section>

    <!-- Service 3 -->
    <section class="scroll-section service-row">
      <div class="service-text animate-up delay-1">
        <span class="service-num">03 / Management</span>
        <h2>Project Contracting</h2>
        <p>
          End-to-end lifecycle management. We provide strict budget oversight, logistical coordination, 
          and supply chain integration to ensure complex projects are delivered seamlessly from the first blueprint 
          to the final handover.
        </p>
        <ul class="feature-list">
          <li>Budget Control</li>
          <li>Logistical Coordination</li>
          <li>Timeline Management</li>
        </ul>
      </div>
      <div class="service-visual animate-up delay-2">
        <div class="image-wrapper">
          <img src="/images/img3.png" alt="Project Contracting" />
        </div>
      </div>
    </section>

    <!-- Service 4 -->
    <section class="scroll-section service-row reverse">
      <div class="service-text animate-up delay-1">
        <span class="service-num">04 / Supply</span>
        <h2>Materials Supply</h2>
        <p>
          To combat the logistical challenges of island development, we produce and process critical materials locally. 
          Our industrial hub provides structural steel processing and manufactures proprietary reinforced concrete blocks.
        </p>
        <ul class="feature-list">
          <li>Reinforced Concrete</li>
          <li>Structural Steel</li>
          <li>Aggregates</li>
        </ul>
      </div>
      <div class="service-visual animate-up delay-2">
        <div class="image-wrapper">
          <img src="/images/img1.png" alt="Materials Supply" />
        </div>
      </div>
    </section>

    <!-- Call to action footer -->
    <section class="scroll-section services-footer">
      <div class="footer-content animate-up delay-1">
        <h2>Have a specialized requirement?</h2>
        <router-link to="/contact" class="btn-primary huge-btn">Consult Our Engineers</router-link>
      </div>
    </section>

  </div>
</template>

<script setup>
import { onMounted, onUnmounted } from 'vue';

let observer = null;
let darkObserver = null;

onMounted(() => {
  observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('in-view');
      }
    });
  }, { threshold: 0.2 });

  document.querySelectorAll('.animate-up').forEach((el) => {
    observer.observe(el);
  });

  // Observe the dark footer section to turn the logo white
  const footerSection = document.querySelector('.services-footer');
  if (footerSection) {
    darkObserver = new IntersectionObserver((entries) => {
      window.dispatchEvent(new CustomEvent('toggle-nav-dark', { detail: entries[0].isIntersecting }));
    }, { threshold: 0.5 });
    darkObserver.observe(footerSection);
  }
});

onUnmounted(() => {
  if (observer) {
    observer.disconnect();
  }
  if (darkObserver) {
    darkObserver.disconnect();
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
.delay-2 { transition-delay: 0.3s; }

.services-page {
  display: flex;
  flex-direction: column;
}

/* Snap Scrolling Setup */
.scroll-section {
  min-height: 100vh;
  scroll-snap-align: start;
  display: flex;
  position: relative;
  overflow: hidden;
}

.services-header {
  background-color: #fcfcfc;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  border-bottom: 1px solid #f0f0f0;
}

.header-content {
  max-width: 1200px;
  padding: 0 40px;
}

.huge-title {
  font-size: 80px;
  line-height: 0.95;
  letter-spacing: -0.05em;
  color: #111;
  margin-bottom: 24px;
}

.subtitle {
  font-size: 22px;
  color: #555;
  line-height: 1.5;
  max-width: 700px;
  margin: 0 auto;
}

.service-row {
  display: flex;
  width: 100%;
}

.service-row.reverse {
  flex-direction: row-reverse;
  background-color: #fafafa;
}

.service-text {
  flex: 1;
  padding: 80px;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.service-num {
  font-size: 14px;
  font-weight: 600;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: #888;
  margin-bottom: 24px;
}

.service-text h2 {
  font-size: 48px;
  letter-spacing: -1px;
  color: #111;
  margin-bottom: 32px;
  line-height: 1.1;
}

.service-text p {
  font-size: 18px;
  color: #555;
  line-height: 1.7;
  margin-bottom: 40px;
  max-width: 600px;
}

.feature-list {
  list-style: none;
  padding: 0;
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.feature-list li {
  font-size: 16px;
  font-weight: 600;
  color: #111;
  display: flex;
  align-items: center;
  gap: 12px;
}

.feature-list li::before {
  content: '';
  width: 6px;
  height: 6px;
  background-color: #111;
  border-radius: 50%;
}

.service-visual {
  flex: 1;
  padding: 80px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.image-wrapper {
  width: 100%;
  height: 100%;
  border-radius: 24px;
  overflow: hidden;
  box-shadow: 0 40px 80px rgba(0,0,0,0.08);
}

.image-wrapper img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.8s ease;
}

.service-row:hover .image-wrapper img {
  transform: scale(1.05);
}

.services-footer {
  text-align: center;
  background-color: #111;
  color: #fff;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.services-footer h2 {
  font-size: 48px;
  margin-bottom: 40px;
  letter-spacing: -1px;
}

.huge-btn {
  font-size: 16px;
  padding: 20px 48px;
  background-color: #fff;
  color: #111;
  display: inline-block;
}

.huge-btn:hover {
  background-color: #f0f0f0;
  transform: scale(1.05);
}

@media (max-width: 1024px) {
  .huge-title { font-size: 48px; }
  .service-text { padding: 40px; }
  .service-text h2 { font-size: 32px; margin-bottom: 16px; }
  .service-text p { font-size: 14px; margin-bottom: 24px; }
  .feature-list li { font-size: 13px; }
  .service-visual { padding: 40px; }
}

@media (max-width: 768px) {
  .huge-title { font-size: 32px; }
  .subtitle { font-size: 14px; padding: 0 20px; }
  
  .service-row { flex-direction: row; align-items: center; min-height: 100vh; padding: 20px; gap: 10px; }
  .service-row.reverse { flex-direction: row-reverse; }
  
  .service-text { padding: 0; flex: 1; align-items: flex-start; text-align: left; }
  .service-text h2 { font-size: 20px; margin-bottom: 12px; letter-spacing: -0.5px; }
  .service-text p { font-size: 11px; margin-bottom: 16px; line-height: 1.4; }
  .service-num { font-size: 10px; margin-bottom: 8px; }
  .feature-list { align-items: flex-start; }
  .feature-list li { font-size: 10px; gap: 6px; }
  
  .service-visual { padding: 0; flex: 1; height: 40vh; }
  .image-wrapper { height: 100%; border-radius: 12px; box-shadow: 0 10px 20px rgba(0,0,0,0.1); }
  
  .services-footer h2 { font-size: 32px; margin-bottom: 20px; }
  .huge-btn { padding: 12px 24px; font-size: 14px; }
}
</style>
