<script setup>
import Header from './components/header.vue';
import Searchbar from './components/searchbar.vue';
import Main from './components/main.vue';
import Product from './components/product.vue';
import Footer from './components/footer.vue';

</script>

<template>
  <Header />

  <Searchbar />

  <Main />

  <Product />

  <Footer />
 
</template>

<style scoped>

/* 💡 တစ်ကမ္ဘာလုံးဆိုင်ရာ CSS ကို အစကနေ ပြန်ညှိခြင်း */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-color: #f0f2f5; /* နောက်ခံကို မီးခိုးနုရောင် အေးအေးလေး ပြောင်းတာပါ */
  font-family: system-ui, -apple-system, sans-serif;
}

.app-wrapper {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

/* 💡 Product Card ကို စခရင်အပြည့်နဲ့ အလယ်တည့်တည့် ရောက်စေမည့် နေရာ */
.content-container {
  flex: 1;
  display: flex;
  justify-content: center; /* ဘယ်/ညာ အလယ်ဗဟို ညှိခြင်း */
  align-items: center;     /* အပေါ်/အောက် အလယ်ဗဟို ညှိခြင်း */
  padding: 80px 20px 40px 20px; /* Nav Bar နဲ့ မငြိအောင် အပေါ်ကို Space ချန်ခြင်း */
  width: 100%;
}

</style>