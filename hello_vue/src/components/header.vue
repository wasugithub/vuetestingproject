<script setup>
import { ref } from 'vue';

const isMenuOpen =ref(false);

const navlinks = ref([
    {name:'Home',url: '#'},
    {name:'About',url: '#'},
    {name:'Service',url: '#'},
    {name:'Contact',url: '#'},
])

const toggleMenu = () =>{
    isMenuOpen.value = !isMenuOpen.value;
}

</script>

<template>
<nav class="navbar">
    <nav class="nav-container">
        <a href="" class="nav-logo">📱 Apple</a>

        <ul class="nav-links" :class="{'nav-active':isMenuOpen}">
            <li v-for="link in navlinks" :key="link.name">
                <a :href="link.url" @click="isMenuOpen = false">{{ link.name }}</a>
            </li>
        </ul>

        <button class="menu-toggle" @click="toggleMenu" aria-label="Toggle navigation">
            <span class="bar" :class="{'animate-top':isMenuOpen}"></span>
            <span class="bar" :class="{'animate-middle':isMenuOpen}"></span>
            <span class="bar" :class="{'animate-bottom':isMenuOpen}"></span>
        </button>
    </nav>
</nav>
</template>

<style scoped>
.navbar {
  background-color: #1a1a2e;
  color: #ffffff;
  padding: 1rem 2rem;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  z-index: 1000;
  box-sizing: border-box;
}

.nav-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: 1200px;
  margin: 0 auto;
  width: 100%;
}

.nav-logo {
  font-size: 1.5rem;
  font-weight: bold;
  color: #42b883; /* Vue Green Color */
  text-decoration: none;
}

/* Links များ (Desktop Version) */
.nav-links {
  display: flex;
  list-style: none;
  gap: 2rem;
  margin: 0;
  padding: 0;
}

.nav-links a {
  color: #e2e8f0;
  text-decoration: none;
  font-size: 1rem;
  transition: color 0.3s ease;
}

.nav-links a:hover {
  color: #42b883;
}

/* Hamburger Menu Button (Desktop မှာ ဖျောက်ထားမည်) */
.menu-toggle {
  display: none;
  flex-direction: column;
  justify-content: space-between;
  width: 24px;
  height: 18px;
  background: transparent;
  border: none;
  cursor: pointer;
  padding: 0;
}

.bar {
  width: 100%;
  height: 3px;
  background-color: #ffffff;
  transition: all 0.3s ease;
}

/* 📱 Mobile UI အပြင်အဆင် (ဖုန်းမျက်နှာပြင်များအတွက်) */
@media (max-width: 768px) {
  .menu-toggle {
    display: flex;
  }

  .nav-links {
    position: absolute;
    top: 100%;
    left: 0;
    width: 100%;
    background-color: #1a1a2e;
    flex-direction: column;
    align-items: center;
    gap: 0;
    max-height: 0;
    overflow: hidden;
    transition: max-height 0.4s ease-in-out;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  }

  /* Hamburger ကို နှိပ်လိုက်ရင် အောက်ကို ပွင့်လာမည့် ပုံစံ */
  .nav-links.nav-active {
    max-height: 300px;
  }

  .nav-links li {
    width: 100%;
    text-align: center;
  }

  .nav-links a {
    display: block;
    padding: 1rem;
    border-top: 1px solid #2d2d44;
  }

  /* Hamburger Icon လေးကို ✖ ပုံစံ ပြောင်းလဲမည့် Animation */
  .animate-top {
    transform: translateY(7px) rotate(45deg);
  }
  .animate-middle {
    opacity: 0;
  }
  .animate-bottom {
    transform: translateY(-8px) rotate(-45deg);
  }
}
</style>