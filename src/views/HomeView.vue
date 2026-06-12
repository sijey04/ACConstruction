<template>
  <div class="home-wrapper">
    <!-- 1. Hero Section -->
    <section class="scroll-section hero-screen">
      <div class="hero-top animate-up delay-1">
        <h1 class="hero-title">AC Construction Co.<br>& Services</h1>
        <p class="hero-subtitle">Leading construction, infrastructure support, land reclamation,<br>and development projects in the Marshall Islands.</p>
      </div>

      <div class="gallery-section animate-up delay-2">
        <div class="gallery-track">
          <div 
            class="gallery-item" 
            v-for="(project, index) in duplicatedProjects" 
            :key="index"
            @click="openModal(project)"
          >
            <div class="image-wrapper">
              <img :src="project.image" :alt="project.title">
              <div class="hover-overlay">
                <span>View Details</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- 2. Introduction Section -->
    <section class="scroll-section intro-section">
      <div class="intro-container">
        <div class="intro-text animate-up delay-1">
          <h2>Building the Future of the Nation</h2>
          <p>
            Established by the Bing family under Kabkondrikdrik Enterprises Inc. (KEI), 
            AC Construction Co. & Services is at the forefront of the Marshall Islands' structural development. 
            We specialize in high-impact public and government contracting services. Our mission is to deliver 
            uncompromising quality while creating sustainable local jobs for our community.
          </p>
        </div>
        <div class="intro-stats">
          <div class="stat-box animate-up delay-2">
            <span class="stat-number">20+</span>
            <span class="stat-label">Years of Excellence</span>
          </div>
          <div class="stat-box animate-up delay-3">
            <span class="stat-number">150+</span>
            <span class="stat-label">Completed Projects</span>
          </div>
          <div class="stat-box animate-up delay-4">
            <span class="stat-number">100%</span>
            <span class="stat-label">Marshallese Owned</span>
          </div>
        </div>
      </div>
    </section>

    <!-- 3. Core Capabilities Section -->
    <section class="scroll-section capabilities-section">
      <div class="capabilities-container">
        <div class="cap-header animate-up delay-1">
          <h2>Core Capabilities</h2>
          <p>Comprehensive engineering and development solutions tailored for the Pacific.</p>
        </div>
        <div class="cap-grid">
          <div class="cap-card animate-up delay-2">
            <h3>Commercial Construction</h3>
            <p>Full-scale construction for private complexes, healthcare facilities, and educational institutions with state-of-the-art engineering.</p>
          </div>
          <div class="cap-card animate-up delay-3">
            <h3>Earthworks & Marine</h3>
            <p>Specializing in heavy land reclamation, seawall construction, and marine infrastructure support using our dedicated fleet.</p>
          </div>
          <div class="cap-card animate-up delay-4">
            <h3>Project Contracting</h3>
            <p>End-to-end project lifecycle management, maintaining strict budget and timeline controls for seamless execution.</p>
          </div>
          <div class="cap-card animate-up delay-5">
            <h3>Materials Supply</h3>
            <p>Manufacturing and supplying high-grade construction materials including reinforced concrete blocks and structural steel.</p>
          </div>
        </div>
      </div>
    </section>

    <!-- 4. Featured Works Section -->
    <section class="scroll-section works-section">
      <div class="works-container">
        <div class="works-header animate-up delay-1">
          <h2>Featured Previous Works</h2>
          <p>A glimpse into our recent milestones in infrastructure and land development.</p>
        </div>
        <div class="works-grid">
          <div class="work-card animate-up" :class="'delay-' + (index + 2)" v-for="(project, index) in projects" :key="project.id" @click="openModal(project)">
            <div class="work-image"><img :src="project.image" :alt="project.title"></div>
            <div class="work-details">
              <h3>{{ project.title }}</h3>
              <p>{{ project.shortDesc }}</p>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Apple-style Premium Modal -->
    <Teleport to="body">
      <transition name="modal-fade">
        <div class="modal-overlay" v-if="selectedProject" @click="closeModal">
          <div class="modal-content-wrapper" @click.stop>
            <div class="modal-content">
              <button class="close-btn" @click="closeModal">
                <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M18 6L6 18M6 6l12 12"/></svg>
              </button>
              
              <div class="modal-image-container">
                <img :src="selectedProject.image" :alt="selectedProject.title" class="modal-img">
              </div>
              
              <div class="modal-info">
                <div class="modal-info-scroll">
                  <h2>{{ selectedProject.title }}</h2>
                  <p class="modal-desc">{{ selectedProject.description }}</p>
                  
                  <div class="modal-divider"></div>
                  
                  <div class="modal-meta-grid">
                    <div class="meta-item">
                      <strong>Client</strong>
                      <span>{{ selectedProject.client }}</span>
                    </div>
                    <div class="meta-item">
                      <strong>Timeline</strong>
                      <span>{{ selectedProject.timeline }}</span>
                    </div>
                    <div class="meta-item full-width">
                      <strong>Project Scope</strong>
                      <span>{{ selectedProject.scope }}</span>
                    </div>
                  </div>

                  <div class="modal-divider"></div>

                  <div class="testimonial-block">
                    <svg class="quote-icon" width="24" height="24" viewBox="0 0 24 24" fill="currentColor"><path d="M14.017 21v-7.391c0-5.704 3.731-9.57 8.983-10.609l.995 2.151c-2.432.917-3.995 3.638-3.995 5.849h4v10h-9.983zm-14.017 0v-7.391c0-5.704 3.748-9.57 9-10.609l.996 2.151c-2.433.917-3.996 3.638-3.996 5.849h3.983v10h-9.983z"/></svg>
                    <p>{{ selectedProject.testimonial }}</p>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </transition>
    </Teleport>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue';

const projects = [
  { 
    id: 1, 
    image: '/images/ac1.png', 
    title: 'Oceanfront Commercial Complex', 
    shortDesc: 'End-to-end structural construction and project management for a state-of-the-art commercial facility.',
    description: 'A flagship commercial project demanding extensive structural steel framework, deep foundation pylons, and sustainable materials. Delivered on schedule despite challenging coastal weather conditions.',
    client: 'KEI Development',
    timeline: 'Q1 2024 - Q4 2025',
    scope: 'Structural Engineering, HVAC, Project Management',
    testimonial: '"AC Construction proved their mastery of Pacific logistics. The complex was delivered exactly to spec, exceeding all our rigorous safety standards." - Director of Development, KEI'
  },
  { 
    id: 2, 
    image: '/images/ac2.png', 
    title: 'Coastal Land Reclamation', 
    shortDesc: 'Extensive earthmoving and marine engineering to secure and expand vital coastal territories.',
    description: 'This critical infrastructure project utilized heavy dredging and soil stabilization techniques to reclaim oceanfront land, providing a solid foundation for future urban expansion while protecting the shoreline.',
    client: 'Government Initiative',
    timeline: 'Q3 2023 - Q2 2024',
    scope: 'Earthworks, Dredging, Marine Engineering',
    testimonial: '"Their heavy civil capabilities are unmatched in the islands. They not only expanded our usable land but fortified our coast against rising tides." - Ministry of Infrastructure'
  },
  { 
    id: 3, 
    image: '/images/ac3.png', 
    title: 'Modern Government Infrastructure', 
    shortDesc: 'Delivered premium, climate-resilient concrete and glass infrastructure for public sector operations.',
    description: 'Designed and built to withstand severe tropical marine conditions, this modern public building features high-grade reinforced concrete, hurricane-resistant glass, and energy-efficient systems.',
    client: 'Public Sector',
    timeline: 'Q2 2022 - Q1 2024',
    scope: 'General Contracting, Bespoke Construction',
    testimonial: '"A stunning addition to our civic infrastructure. AC Construction delivered a facility that is both beautiful and built to last generations." - Civic Planning Board'
  },
  { 
    id: 4, 
    image: '/images/ac4.png', 
    title: 'Materials Manufacturing Hub', 
    shortDesc: 'Large scale industrial site producing high-quality concrete blocks and steel rebars.',
    description: 'To support our ongoing projects and the local economy, we built this manufacturing hub. It produces our proprietary reinforced concrete blocks and processes structural steel directly on the island.',
    client: 'AC Internal Logistics',
    timeline: 'Q1 2021 - Q4 2021',
    scope: 'Industrial Facility, Concrete Production',
    testimonial: '"This hub revolutionized our supply chain. By manufacturing locally, we bypass international shipping delays and guarantee uncompromised material quality." - Head of Operations, AC Construction'
  },
];

const duplicatedProjects = [...projects, ...projects, ...projects];
const selectedProject = ref(null);
let observer = null;

onMounted(() => {
  observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('in-view');
      }
    });
  }, { threshold: 0.15 });

  document.querySelectorAll('.animate-up').forEach((el) => {
    observer.observe(el);
  });
});

onUnmounted(() => {
  if (observer) {
    observer.disconnect();
  }
});

const openModal = (project) => {
  selectedProject.value = project;
  document.body.style.overflow = 'hidden';
};

const closeModal = () => {
  selectedProject.value = null;
  document.body.style.overflow = '';
};
</script>

<style scoped>
.home-wrapper {
  display: flex;
  flex-direction: column;
}

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
.delay-4 { transition-delay: 0.55s; }
.delay-5 { transition-delay: 0.7s; }

/* Snap Scrolling Setup */
.scroll-section {
  min-height: 100vh; /* Full viewport */
  scroll-snap-align: start;
  display: flex;
  flex-direction: column;
  justify-content: center;
  position: relative;
  overflow: hidden;
  padding: 40px 0; /* Add generous padding to properly space contents internally */
}

/* 1. Hero Screen */
.hero-screen {
  position: relative;
  justify-content: flex-start;
  padding: 0 !important; /* Override the 40px scroll-section padding */
}

.hero-top {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  flex: 0 0 auto;
  margin-top: 14vh; /* Clear the transparent navbar */
  margin-bottom: 3vh;
}

.gallery-section {
  flex: 1; /* Stretch to the very bottom */
  position: relative;
  background-color: #f5f5f5;
  overflow: hidden;
}

.gallery-section::before,
.gallery-section::after {
  content: '';
  position: absolute;
  left: -20%;
  width: 140%;
  height: 250px;
  background-color: var(--bg-color, #fff);
  border-radius: 50%;
  z-index: 10;
  pointer-events: none;
}
.gallery-section::before { top: -180px; }
.gallery-section::after { bottom: -120px; } /* Deep white pocket at the bottom */



@keyframes scrollGallery {
  0% { transform: translateX(0); }
  100% { transform: translateX(calc(-100% / 3)); }
}

.gallery-track {
  display: flex;
  width: max-content; 
  height: 100%;
  gap: 12px;
  padding: 0 12px;
  animation: scrollGallery 80s linear infinite;
}

.gallery-section:hover .gallery-track {
  animation-play-state: paused;
}

.gallery-item {
  width: 400px; 
  height: 100%;
  position: relative;
  overflow: hidden;
  border-radius: 4px;
  cursor: pointer;
}

.image-wrapper {
  width: 100%;
  height: 100%;
  position: relative;
}

.gallery-item img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.8s cubic-bezier(0.16, 1, 0.3, 1);
}

.hover-overlay {
  position: absolute;
  top: 0; left: 0; right: 0; bottom: 0;
  background: rgba(0,0,0,0.3);
  backdrop-filter: blur(2px);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 0.4s ease;
}

.hover-overlay span {
  color: #fff;
  font-weight: 500;
  font-size: 15px;
  letter-spacing: 0.5px;
  padding: 12px 24px;
  border-radius: 40px;
  background: rgba(255, 255, 255, 0.1);
  border: 1px solid rgba(255, 255, 255, 0.4);
  backdrop-filter: blur(8px);
}

.gallery-item:hover img { transform: scale(1.04); }
.gallery-item:hover .hover-overlay { opacity: 1; }

/* 2. Intro Section */
.intro-section {
  background-color: #fafafa;
}

.intro-container {
  max-width: 1000px;
  margin: 0 auto;
  display: flex;
  align-items: center;
  gap: 60px;
  padding: 0 40px;
}

.intro-text {
  flex: 1.2;
}

.intro-text h2 {
  font-size: 40px;
  margin-bottom: 24px;
  letter-spacing: -1px;
}

.intro-text p {
  font-size: 17px;
  line-height: 1.7;
  color: #555;
}

.intro-stats {
  flex: 1;
  display: grid;
  grid-template-columns: 1fr;
  gap: 24px;
}

.stat-box {
  background: #fff;
  padding: 32px;
  border-radius: 16px;
  box-shadow: 0 10px 30px rgba(0,0,0,0.03);
  display: flex;
  flex-direction: column;
  border: 1px solid #eee;
}

.stat-number {
  font-size: 48px;
  font-weight: 800;
  color: #111;
  margin-bottom: 8px;
}

.stat-label {
  font-size: 14px;
  color: #666;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: 600;
}

/* 3. Capabilities Section */
.capabilities-section {
  background-color: #fff;
}

.capabilities-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 40px;
  width: 100%;
}

.cap-header {
  text-align: center;
  margin-bottom: 40px;
}

.cap-header h2 {
  font-size: 32px;
  margin-bottom: 12px;
}

.cap-header p {
  font-size: 16px;
  color: #666;
}

.cap-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 20px;
}

.cap-card {
  background: #fafafa;
  padding: 24px 32px;
  border-radius: 16px;
  border: 1px solid #eee;
  transition: transform 0.3s ease;
}

.cap-card:hover {
  transform: translateY(-4px);
  background: #f0f0f0;
}

.cap-card h3 {
  font-size: 20px;
  margin-bottom: 10px;
  color: #111;
}

.cap-card p {
  font-size: 14.5px;
  color: #555;
  line-height: 1.5;
}

/* 4. Works Section */
.works-section {
  background-color: #fcfcfc;
}

.works-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 40px;
  width: 100%;
}

.works-header {
  text-align: center;
  margin-bottom: 60px;
}

.works-header h2 {
  font-size: 40px;
  margin-bottom: 16px;
}

.works-header p {
  font-size: 18px;
  color: #666;
}

.works-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 24px;
}

.work-card {
  background: #fff;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 10px 20px rgba(0,0,0,0.03);
  transition: transform 0.4s cubic-bezier(0.16, 1, 0.3, 1), box-shadow 0.4s ease;
  cursor: pointer;
  border: 1px solid #eee;
}

.work-card:hover {
  transform: translateY(-8px) scale(1.01);
  box-shadow: 0 20px 40px rgba(0,0,0,0.08);
}

.work-image {
  height: 200px;
  overflow: hidden;
}

.work-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.6s cubic-bezier(0.16, 1, 0.3, 1);
}

.work-card:hover .work-image img {
  transform: scale(1.05);
}

.work-details {
  padding: 24px;
}

.work-details h3 {
  font-size: 18px;
  margin-bottom: 8px;
  font-weight: 700;
  letter-spacing: -0.5px;
}

.work-details p {
  font-size: 14px;
  color: #666;
  line-height: 1.5;
}

/* Modal */
.modal-overlay {
  position: fixed;
  top: 0; left: 0; right: 0; bottom: 0;
  background: rgba(0,0,0,0.4); 
  backdrop-filter: blur(12px); 
  z-index: 1000;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 40px;
}

.modal-content-wrapper {
  width: 100%;
  max-width: 1000px;
  transform: translateZ(0); 
}

.modal-content {
  background: rgba(255, 255, 255, 0.85); 
  backdrop-filter: blur(30px) saturate(150%);
  border: 1px solid rgba(255,255,255,0.4);
  width: 100%;
  border-radius: 24px; 
  overflow: hidden;
  display: flex;
  position: relative;
  box-shadow: 0 40px 100px rgba(0,0,0,0.2), 0 10px 40px rgba(0,0,0,0.05);
  max-height: 85vh; /* Constrain height so scrolling activates */
}

.close-btn {
  position: absolute;
  top: 20px; right: 20px;
  background: rgba(255, 255, 255, 0.25);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border: 1px solid rgba(255, 255, 255, 0.6);
  width: 40px; height: 40px;
  border-radius: 50%;
  color: #fff;
  cursor: pointer;
  z-index: 100;
  display: flex; align-items: center; justify-content: center;
  transition: all 0.2s ease;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
}

.close-btn:hover {
  background: rgba(255, 255, 255, 0.4);
  transform: scale(1.05);
}

.modal-image-container {
  flex: 1.3;
  position: relative;
}

.modal-image-container::after {
  content: '';
  position: absolute;
  top: 0; right: 0; bottom: 0;
  width: 1px;
  background: linear-gradient(to bottom, transparent, rgba(0,0,0,0.05), transparent);
}

.modal-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

.modal-info {
  flex: 1;
  display: flex;
  flex-direction: column;
  overflow: hidden;
}

.modal-info-scroll {
  padding: 48px 40px;
  overflow-y: auto;
  display: flex;
  flex-direction: column;
  justify-content: flex-start; /* Ensure long content starts at top */
}

.modal-info h2 {
  font-size: 32px;
  font-weight: 700;
  letter-spacing: -0.8px;
  margin-bottom: 16px;
  line-height: 1.1;
  color: #111;
}

.modal-desc {
  font-size: 16px;
  color: #444;
  line-height: 1.6;
  margin-bottom: 32px;
}

.modal-divider {
  height: 1px;
  background: rgba(0,0,0,0.06);
  margin-bottom: 32px;
}

.modal-meta-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 24px;
}

.meta-item {
  display: flex;
  flex-direction: column;
}

.meta-item strong {
  font-size: 11px;
  color: #888;
  text-transform: uppercase;
  letter-spacing: 1px;
  margin-bottom: 6px;
  font-weight: 600;
}

.meta-item span {
  font-size: 15px;
  color: #111;
  font-weight: 500;
}

.meta-item.full-width {
  grid-column: 1 / -1;
}

.testimonial-block {
  background: rgba(0,0,0,0.03);
  padding: 24px;
  border-radius: 12px;
  position: relative;
}

.quote-icon {
  color: rgba(0,0,0,0.1);
  margin-bottom: 12px;
}

.testimonial-block p {
  font-size: 15px;
  font-style: italic;
  color: #333;
  line-height: 1.6;
}

/* Transitions */
.modal-fade-enter-active {
  transition: all 0.5s cubic-bezier(0.16, 1, 0.3, 1);
}
.modal-fade-leave-active {
  transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
}
.modal-fade-enter-from, .modal-fade-leave-to {
  opacity: 0;
}
.modal-fade-enter-from .modal-content-wrapper {
  transform: scale(0.96) translateY(20px);
}
.modal-fade-leave-to .modal-content-wrapper {
  transform: scale(0.98);
}

@media (max-width: 900px) {
  .hero-title { font-size: 40px; }
  .hero-subtitle { font-size: 14px; }
  .intro-text h2 { font-size: 28px; margin-bottom: 16px; }
  .intro-text p { font-size: 13px; }
  .stat-number { font-size: 32px; }
  .stat-box { padding: 20px; }
  .cap-card { padding: 16px 20px; }
  .cap-card h3 { font-size: 16px; }
  .cap-card p { font-size: 12px; }
  .works-header h2 { font-size: 28px; }
  .works-header p { font-size: 14px; }
  .work-details h3 { font-size: 16px; }
  .work-details p { font-size: 12px; }
  .gallery-item { width: 200px; }
  .modal-content { max-height: 85vh; }
  .modal-image-container { flex: 1; }
  .modal-info-scroll { padding: 24px; }
}

@media (max-width: 768px) {
  .hero-top { margin-top: 15vh; margin-bottom: 8vh; }
  .hero-title { font-size: 40px; }
  .hero-subtitle { font-size: 14px; padding: 0 20px; line-height: 1.5; }
  .intro-container { gap: 40px; padding: 0 20px; flex-direction: column; }
  .intro-text h2 { font-size: 28px; }
  .intro-text p { font-size: 14px; }
  .intro-stats { gap: 16px; }
  .stat-number { font-size: 32px; }
  .stat-label { font-size: 12px; }
  .stat-box { padding: 20px; }
  .capabilities-container, .works-container { padding: 0 20px; }
  .cap-header h2 { font-size: 28px; }
  .cap-header p { font-size: 14px; }
  .works-header h2 { font-size: 28px; margin-bottom: 10px; }
  .works-grid { gap: 20px; }
  .work-image { height: 180px; }
  .work-details { padding: 20px; }
  .gallery-section { height: 35vh; }
  .gallery-section::before { top: -60px; height: 100px; width: 160%; left: -30%; }
  .gallery-section::after { bottom: -60px; height: 100px; width: 160%; left: -30%; }

  .modal-overlay { padding: 16px; }
  .modal-content { flex-direction: column; width: 100%; height: 85vh; border-radius: 16px; }
  .modal-image-container { height: 30vh; flex: none; }
  .modal-image-container::after { display: none; }
  .modal-info { overflow: hidden; }
  .modal-info-scroll { padding: 24px; flex: 1; min-height: 0; overflow-y: auto; }
  .modal-info h2 { font-size: 24px; margin-bottom: 12px; }
  .modal-desc { font-size: 14px; margin-bottom: 24px; }
  .modal-meta-grid { grid-template-columns: 1fr; gap: 16px; }
  .meta-item strong { font-size: 11px; margin-bottom: 4px; }
  .meta-item span { font-size: 14px; }
  .testimonial-block { padding: 16px; }
  .testimonial-block p { font-size: 13px; }
}
</style>
