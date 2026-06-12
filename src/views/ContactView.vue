<template>
  <div class="contact-page">
    <div class="contact-container">
      
      <div class="contact-left animate-up delay-1">
        <div class="left-content">
          <h1 class="huge-title">Let's build<br>together.</h1>
          <p class="subtitle">Whether you have a specific project in mind or simply want to explore possibilities, our engineering team is ready to assist you.</p>
          
          <div class="contact-info">
            <div class="info-block">
              <span class="info-label">Headquarters</span>
              <p>Kabkondrikdrik Enterprises Inc.<br>Majuro, Marshall Islands 96960</p>
            </div>
            <div class="info-block">
              <span class="info-label">Direct Line</span>
              <p><a href="#" class="hover-link">+692 000 0000</a></p>
            </div>
            <div class="info-block">
              <span class="info-label">Email Inquiries</span>
              <p><a href="#" class="hover-link">info@acconstruction.com</a></p>
            </div>
          </div>
        </div>
      </div>
      
      <div class="contact-right animate-up delay-2">
        <div class="form-card">
          <h2>Send a Message</h2>
          <form class="contact-form" @submit.prevent="submitForm">
            <div class="input-row">
              <div class="form-group">
                <label>First Name</label>
                <input type="text" placeholder="John" required />
              </div>
              <div class="form-group">
                <label>Last Name</label>
                <input type="text" placeholder="Doe" required />
              </div>
            </div>
            
            <div class="form-group">
              <label>Email Address</label>
              <input type="email" placeholder="john@company.com" required />
            </div>
            
            <div class="form-group">
              <label>Project Scope</label>
              <select required>
                <option value="" disabled selected>Select an option...</option>
                <option value="commercial">Commercial Construction</option>
                <option value="reclamation">Land Reclamation</option>
                <option value="materials">Materials Supply</option>
                <option value="other">Other Inquiry</option>
              </select>
            </div>

            <div class="form-group">
              <label>Message</label>
              <textarea placeholder="Tell us about your project..." rows="3" required></textarea>
            </div>
            
            <button type="submit" class="submit-btn">
              <span>Submit Inquiry</span>
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="5" y1="12" x2="19" y2="12"></line><polyline points="12 5 19 12 12 19"></polyline></svg>
            </button>
          </form>
        </div>
      </div>

    </div>
  </div>
</template>

<script setup>
import { onMounted } from 'vue';

const submitForm = () => {
  alert('Thank you for reaching out. Our team will contact you shortly.');
};

onMounted(() => {
  // Trigger animation simply on mount since it's a fixed page
  setTimeout(() => {
    document.querySelectorAll('.animate-up').forEach(el => el.classList.add('in-view'));
  }, 100);
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

/* Contact Page Fixed Height */
.contact-page {
  height: 100vh; /* Fixed single page height */
  overflow: hidden; /* Prevent any scrolling */
  background-color: #f5f5f5;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0 40px;
}

.contact-container {
  max-width: 1400px;
  width: 100%;
  display: flex;
  gap: 80px;
  align-items: center;
  margin-top: 60px; /* Push down to clear the fixed transparent topbar */
}

/* Left Side */
.contact-left {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.left-content {
  max-width: 600px;
}

.huge-title {
  font-size: 80px;
  line-height: 0.95;
  letter-spacing: -0.05em;
  color: #111;
  margin-bottom: 24px;
}

.subtitle {
  font-size: 18px;
  color: #555;
  line-height: 1.6;
  margin-bottom: 60px;
}

.contact-info {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 40px;
}

.info-block {
  display: flex;
  flex-direction: column;
}

.info-label {
  font-size: 12px;
  text-transform: uppercase;
  letter-spacing: 1.5px;
  color: #888;
  font-weight: 600;
  margin-bottom: 12px;
}

.info-block p, .info-block a {
  font-size: 16px;
  color: #111;
  line-height: 1.5;
  font-weight: 500;
}

.hover-link {
  position: relative;
  display: inline-block;
}

.hover-link::after {
  content: '';
  position: absolute;
  bottom: -2px;
  left: 0;
  width: 100%;
  height: 1px;
  background-color: #111;
  transform: scaleX(0);
  transform-origin: right;
  transition: transform 0.3s ease;
}

.hover-link:hover::after {
  transform: scaleX(1);
  transform-origin: left;
}

/* Right Side Form */
.contact-right {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
}

.form-card {
  background: #fff;
  padding: 50px;
  border-radius: 24px;
  width: 100%;
  max-width: 600px;
  box-shadow: 0 40px 80px rgba(0,0,0,0.06);
}

.form-card h2 {
  font-size: 28px;
  margin-bottom: 32px;
  color: #111;
}

.contact-form {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.input-row {
  display: flex;
  gap: 20px;
}

.input-row .form-group {
  flex: 1;
}

.form-group {
  display: flex;
  flex-direction: column;
}

.form-group label {
  font-size: 13px;
  font-weight: 600;
  color: #666;
  margin-bottom: 8px;
}

.form-group input,
.form-group select,
.form-group textarea {
  width: 100%;
  padding: 14px 20px;
  background: #fafafa;
  border: 1px solid #e0e0e0;
  border-radius: 12px;
  font-family: 'Inter', sans-serif;
  font-size: 15px;
  color: #111;
  transition: all 0.2s ease;
}

.form-group input:focus,
.form-group select:focus,
.form-group textarea:focus {
  outline: none;
  border-color: #111;
  background: #fff;
  box-shadow: 0 4px 12px rgba(0,0,0,0.05);
}

.form-group textarea {
  resize: none;
}

.submit-btn {
  margin-top: 10px;
  background: #111;
  color: #fff;
  border: none;
  padding: 18px;
  border-radius: 12px;
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 12px;
  transition: all 0.3s ease;
}

.submit-btn:hover {
  background: #333;
  transform: translateY(-2px);
  box-shadow: 0 10px 20px rgba(0,0,0,0.1);
}

@media (max-width: 1024px) {
  .huge-title { font-size: 40px; }
  .subtitle { font-size: 14px; margin-bottom: 30px; }
  .contact-container { gap: 40px; margin-top: 80px; }
  .form-card { padding: 30px; }
  .form-card h2 { font-size: 20px; margin-bottom: 20px; }
  .form-group input, .form-group select, .form-group textarea { padding: 10px 14px; font-size: 13px; }
  .info-block p, .info-block a { font-size: 13px; }
  .info-label { font-size: 10px; margin-bottom: 8px; }
}

@media (max-width: 768px) {
  .contact-page { padding: 80px 20px 40px; height: auto; overflow: visible; display: block; background-color: #fcfcfc; }
  .contact-container { flex-direction: column; gap: 30px; margin-top: 0; }
  
  .text-side { display: flex; flex-direction: column; align-items: center; text-align: center; padding: 0; }
  .huge-title { font-size: 36px; margin-bottom: 8px; letter-spacing: -1px; }
  .subtitle { font-size: 14px; margin-bottom: 24px; line-height: 1.5; }
  
  .contact-info { display: flex; flex-direction: row; flex-wrap: wrap; justify-content: center; gap: 12px; }
  .info-block { flex: 1 1 45%; background: #fff; padding: 16px; border-radius: 12px; box-shadow: 0 4px 12px rgba(0,0,0,0.03); text-align: center; }
  .info-label { font-size: 10px; color: #888; margin-bottom: 4px; display: block; }
  .info-block p, .info-block a { font-size: 12px; font-weight: 600; color: #111; }
  
  .form-side { width: 100%; margin-top: 10px; }
  .form-card { padding: 24px; background: #fff; border-radius: 20px; box-shadow: 0 10px 30px rgba(0,0,0,0.05); }
  .form-card h2 { font-size: 20px; text-align: center; margin-bottom: 20px; }
  
  .input-row { flex-direction: column; gap: 12px; }
  .form-group { gap: 6px; }
  .form-group label { font-size: 12px; margin-left: 4px; }
  .form-group input, .form-group select, .form-group textarea { padding: 14px 16px; font-size: 14px; border-radius: 12px; background: #fafafa; border: 1px solid #eee; }
  .form-group textarea { height: 120px; }
  
  .submit-btn { width: 100%; border-radius: 30px; padding: 16px; font-size: 15px; font-weight: 600; margin-top: 8px; }
}
</style>
