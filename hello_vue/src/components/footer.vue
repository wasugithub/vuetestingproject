<script setup>
import {ref} from 'vue'

const currentYear = ref(new Date().getFullYear())

const quickLinks = ref([
    { name: 'Home', url: '#' },
  { name: 'About Us', url: '#' },
  { name: 'Products', url: '#' },
  { name: 'Contact', url: '#' }
])

const supportlinks = ref([
    { name: 'FAQ', url: '#' },
  { name: 'Shipping Policy', url: '#' },
  { name: 'Return & Refund', url: '#' },
  { name: 'Privacy Policy', url: '#' }
])
</script>

<template>
    <footer class="footer">
        <div class="footer-container">

            <div class="footer-col brand-info">
                <h3 class="footer-logo">📱 VueShop</h3>
                <p class="brand-desc">
                    နောက်ဆုံးပေါ် စမတ်ဖုန်းများနှင့် အကောင်းဆုံး နည်းပညာပစ္စည်းများကို ယုံကြည်စိတ်ချစွာ တစ်နေရာတည်းတွင် ဝယ်ယူရရှိနိုင်ပါသည်။
                </p>
                <div class="social-icons">
                    <a href="#" class="social-icon">🌐</a>
          <a href="#" class="social-icon">📘</a>
          <a href="#" class="social-icon">📸</a>
          <a href="#" class="social-icon">🐦</a>
                </div>
            </div>

            <div class="footer-col">
                <h4>Quick Links</h4>
                <ul class="footer-links">
                    <li v-for="link in quickLinks" :key="link.name">
                        <a :href="link.url">{{ link.name }}</a>
                    </li>
                </ul>
            </div>

            <div class="footer-col">
                <h4>Customer Support</h4>
                <ul class="footer-links">
                    <li v-for="link in supportlinks" :key="link.name">
                        <a :href="link.url">{{ link.name }}</a>
                    </li>
                </ul>
                </div>

                <div class="footer-col contact-info">
                    <h4>dontact Us</h4>
                    <p>📍 လမ်း ၃၀၊ ရန်ကုန်မြို့၊ မြန်မာနိုင်ငံ။</p>
        <p>📞 Phone: +95 9 123456789</p>
        <p>✉️ Email: info@vueshop.com</p>
                </div>

        </div>

        <div class="footer-bottom">
            <p>&copy; {{ currentYear }} VueShop. All rights reserved. Built with Vue 3.</p>
        </div>


    </footer>
</template>

<style scoped>
    .footer {
  background-color: #1a202c; /* အမည်းရောင်/မီးခိုးရင့်ရောင် နောက်ခံ */
  color: #a0aec0;
  padding: 4rem 2rem 1.5rem 2rem;
  font-family: system-ui, -apple-system, sans-serif;
  margin-top: auto; /* အမြဲတမ်း အောက်ခြေမှာ ကပ်နေစေရန် */
  width: 100%;
}

.footer-container {
  max-width: 1200px;
  margin: 0 auto;
  display: grid;
  /* 💡 CSS Grid ဖြင့် ကွန်ပျူတာ Screen ပေါ်တွင် Column ၄ ခု ညီတူညီမျှ ခွဲခြင်း */
  grid-template-columns: 2fr 1fr 1fr 1.5fr;
  gap: 3rem;
}

.footer-col h4 {
  color: #ffffff;
  font-size: 1.1rem;
  font-weight: 700;
  margin-bottom: 1.5rem;
  position: relative;
}

/* ခေါင်းစဉ်အောက်က အစိမ်းရောင်လိုင်းလေး */
.footer-col h4::after {
  content: '';
  position: absolute;
  left: 0;
  bottom: -6px;
  width: 35px;
  height: 2px;
  background-color: #42b883; 
}

.footer-logo {
  color: #42b883; /* Vue Green Color */
  font-size: 1.5rem;
  font-weight: bold;
  margin-bottom: 1rem;
}

.brand-desc {
  line-height: 1.6;
  font-size: 0.95rem;
  margin-bottom: 1.5rem;
}

/* Links အလှဆင်ခြင်း */
.footer-links {
  list-style: none;
  padding: 0;
  margin: 0;
}

.footer-links li {
  margin-bottom: 0.75rem;
}

.footer-links a {
  color: #a0aec0;
  text-decoration: none;
  transition: color 0.2s, padding-left 0.2s;
  font-size: 0.95rem;
  display: inline-block;
}

/* Hover လုပ်ရင် စာသားလေးက အစိမ်းရောင်ပြောင်းပြီး ညာဘက်ကို နည်းနည်း တိုးသွားမည့် Animation */
.footer-links a:hover {
  color: #42b883;
  padding-left: 6px;
}

/* Contact Info */
.contact-info p {
  font-size: 0.95rem;
  margin-bottom: 0.75rem;
  line-height: 1.5;
}

/* Social Icons */
.social-icons {
  display: flex;
  gap: 1rem;
}

.social-icon {
  background: #2d3748;
  width: 38px;
  height: 38px;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 50%;
  text-decoration: none;
  font-size: 1.1rem;
  transition: background 0.2s, transform 0.2s;
}

.social-icon:hover {
  background: #42b883;
  transform: translateY(-3px);
}

/* Copyright Bottom Bar */
.footer-bottom {
  max-width: 1200px;
  margin: 3rem auto 0 auto;
  padding-top: 1.5rem;
  border-top: 1px solid #2d3748;
  text-align: center;
  font-size: 0.85rem;
}

/* 📱 Responsive UI (ဖုန်းနှင့် Tablet များအတွက် အလိုအလျောက် ညှိပေးမည့်စနစ်) */
@media (max-width: 900px) {
  .footer-container {
    grid-template-columns: 1fr 1fr; /* Tablet ပေါ်တွင် ၁ တန်း ၂ ခု */
    gap: 2rem;
  }
}

@media (max-width: 600px) {
  .footer-container {
    grid-template-columns: 1fr; /* ဖုန်းပေါ်တွင် ၁ တန်း ၁ ခု ဒေါင်လိုက်စီခြင်း */
    gap: 2rem;
  }
  .footer {
    padding: 3rem 1.5rem 1.5rem 1.5rem;
  }
}
</style>