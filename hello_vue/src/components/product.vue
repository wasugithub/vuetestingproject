<script setup>
import {ref, computed } from 'vue'

const cartCount =ref(0);

const products = ref([
    {
        id: 1,
    name: 'VuePhone 15 Pro',
    price: 999,
    image: 'https://images.unsplash.com/photo-1695048133142-1a20484d2569?w=500&auto=format&fit=crop&q=60',
    tag: 'Trending'
    },
    {
    id: 2,
    name: 'VuePhone 15 Ultra',
    price: 1199,
    image: 'https://images.unsplash.com/photo-1616348436168-de43ad0db179?w=500&auto=format&fit=crop&q=60',
    tag: 'Best Choice'
  },
  {
    id: 3,
    name: 'VuePhone 15 Mini',
    price: 699,
    image: 'https://images.unsplash.com/photo-1510557880182-3d4d3cba35a5?w=500&auto=format&fit=crop&q=60',
    tag: 'Budget King'
  }
])

const addToCart = (productName) => {
    cartCount.value++ 
    alert('🛒 ${productName} ကို ဈေးဝယ်ခြင်းတောင်းထဲ ထည့်လိုက်ပါပြီ!')
}
</script>

<template>
<div class="shop-wrapper">

    <div class="shop-header">
        <h2>Featured Products</h2>
        <div class="cart-icon-wrapper">
            <span class="cart-icon">🛒</span>
            <span class="cart-badge" v-if="cartCount > 0">{{ cartCount }}</span>
        </div>
    </div>

    <div class="product-grid">
        <div v-for="product in products" :key="product.id" class="product-card"> 
            <div class="image-wrapper">
                <span class="product image" >{{ product.tag }}</span>
                <img :src="product.image" :alt="product.name" class="product-img">
            </div>

            <div class="card-body">
                <h3 class="product-name">{{ product.name }}</h3>
                <p class="product-price">{{ product.price }}</p>

                <button class="add-to-cart-btn" @click="addToCart(product.name)">
                    Add to Cart
                </button>
            </div>
        </div>
    </div>
</div>
</template>

<style scoped>
.shop-wrapper {
  max-width: 1200px;
  width: 100%;
  margin: 0 auto;
  padding: 2rem;
  font-family: system-ui, -apple-system, sans-serif;
}

/* Shop Header & Cart Icon CSS */
.shop-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 2rem;
  border-bottom: 2px solid #edf2f7;
  padding-bottom: 1rem;
}

.shop-header h2 {
  font-size: 1.75rem;
  color: #1a202c;
  font-weight: 700;
}

.cart-icon-wrapper {
  position: relative;
  font-size: 1.75rem;
  cursor: pointer;
  background: white;
  padding: 0.5rem;
  border-radius: 50%;
  box-shadow: 0 4px 10px rgba(0,0,0,0.05);
}

.cart-badge {
  position: absolute;
  top: -5px;
  right: -5px;
  background-color: #e53e3e;
  color: white;
  font-size: 0.75rem;
  font-weight: bold;
  padding: 0.25rem 0.5rem;
  border-radius: 50%;
  min-width: 18px;
  text-align: center;
}

/* 💡 CSS Grid နည်းပညာဖြင့် တစ်တန်းလျှင် ကတ် ၃ ခု စီခြင်း */
.product-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr); /* ကော်လံ ၃ ခု ညီတူညီမျှ ခွဲခြင်း */
  gap: 2rem; /* ကတ်တစ်ခုနှင့်တစ်ခုကြား အကွာအဝေး */
}

/* Product Card တစ်ခုချင်းစီ၏ အလှဆင်ခြင်း */
.product-card {
  background: #ffffff;
  border-radius: 16px;
  overflow: hidden;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.05);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  display: flex;
  flex-direction: column;
}

.product-card:hover {
  transform: translateY(-5px); /* Hover လုပ်လျှင် အပေါ်သို့ အနည်းငယ် ကြွတက်ခြင်း */
  box-shadow: 0 12px 30px rgba(0, 0, 0, 0.1);
}

.image-wrapper {
  position: relative;
  height: 250px;
  background: #f7fafc;
  overflow: hidden;
}

.product-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.product-tag {
  position: absolute;
  top: 12px;
  left: 12px;
  background: #42b883;
  color: white;
  font-size: 0.75rem;
  font-weight: 700;
  padding: 0.25rem 0.75rem;
  border-radius: 50px;
  z-index: 10;
}

.card-body {
  padding: 1.5rem;
  display: flex;
  flex-direction: column;
  flex-grow: 1;
}

.product-name {
  font-size: 1.25rem;
  color: #2d3748;
  margin: 0 0 0.5rem 0;
  font-weight: 600;
}

.product-price {
  font-size: 1.4rem;
  color: #42b883;
  font-weight: 700;
  margin-bottom: 1.5rem;
}

/* Add to Cart Button CSS */
.add-to-cart-btn {
  margin-top: auto; /* ခလုတ်ကို ကတ်၏ အောက်ခြေတွင် အမြဲတစ်သားတည်း ရှိနေစေရန် */
  background-color: #35495e;
  color: white;
  border: none;
  padding: 0.75rem;
  font-size: 1rem;
  font-weight: 600;
  border-radius: 8px;
  cursor: pointer;
  transition: background-color 0.2s;
}

.add-to-cart-btn:hover {
  background-color: #42b883;
}

/* 📱 Mobile Responsive (ဖုန်းဖြင့်ကြည့်လျှင် တစ်တန်းကို ၁ ခုပဲ ပြောင်းပေးမည့်စနစ်) */
@media (max-width: 900px) {
  .product-grid {
    grid-template-columns: repeat(2, 1fr); /* Tablet ပေါ်တွင် ၁ တန်း ၂ ခု */
  }
}

@media (max-width: 600px) {
  .product-grid {
    grid-template-columns: 1fr; /* ဖုန်းပေါ်တွင် ၁ တန်း ၁ ခု ပြောင်းလဲခြင်း */
    gap: 1.5rem;
  }
}
</style>