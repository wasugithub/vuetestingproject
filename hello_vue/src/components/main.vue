<script setup>
import { ref, computed} from 'vue'

const phoneVariants = ref([
    {id: 1, color: 'Deep Purple', hex: '#4b3d60', image: 'https://images.unsplash.com/photo-1695048133142-1a20484d2569?w=500&auto=format&fit=crop&q=60'},
    { id: 2, color: 'Space Black', hex: '#212224', image: 'https://images.unsplash.com/photo-1616348436168-de43ad0db179?w=500&auto=format&fit=crop&q=60' },
    { id: 3, color: 'Silver', hex: '#e3e4e5', image: 'https://images.unsplash.com/photo-1510557880182-3d4d3cba35a5?w=500&auto=format&fit=crop&q=60' }
])

const selectedVariant = ref(phoneVariants.value[0])
const quantity =ref(1);
const basePrice =999

const totalPrice = computed(() => {
    return basePrice * quantity.value
})

const selectColor= (variant) => {
    selectedVariant.value = variant
}

const handleBuy = () => {
   alert(`🎉 ဝယ်ယူမှု အောင်မြင်ပါသည်!\n\nကုန်ပစ္စည်း: VuePhone 15 Pro (${selectedVariant.value.color})\nအရေအတွက်: ${quantity.value} လုံး\nစုစုပေါင်းကျသင့်ငွေ: $${totalPrice.value}`)
}
</script>
<template>
  <div class="product-container">
    <!-- ဘယ်ဘက်ခြမ်း - ဖုန်းဓာတ်ပုံ ပြသမည့်အပိုင်း -->
    <div class="image-gallery">
      <div class="main-image-wrapper">
        <img :src="selectedVariant.image" :alt="selectedVariant.color" class="product-image" />
      </div>
    </div>

    <!-- ညာဘက်ခြမ်း - အသေးစိတ်အချက်အလက်များနှင့် Buy Button အပိုင်း -->
    <div class="product-details">
      <span class="badge">New Release</span>
      <h1 class="product-title">VuePhone 15 Pro</h1>
      
      <p class="product-description">
        နောက်ဆုံးပေါ် Titanium ကိုယ်ထည်၊ စွမ်းအားမြင့် A17 Pro Chip အပြင် ကမ္ဘာ့အကောင်းဆုံး ကင်မရာစနစ်တို့ ပါဝင်လာတဲ့ စမတ်ဖုန်းကောင်းတစ်လုံး ဖြစ်ပါတယ်။
      </p>

      <!-- ဈေးနှုန်း ပြသမည့်နေရာ -->
      <div class="price-section">
        <span class="current-price">${{ basePrice }}</span>
        <span class="original-price">$1199</span>
      </div>

      <hr class="divider" />

      <!-- အရောင်ရွေးချယ်ရန် နေရာ -->
      <div class="option-section">
        <h3>Select Color: <span class="color-name">{{ selectedVariant.color }}</span></h3>
        <div class="color-picker">
          <button 
            v-for="variant in phoneVariants" 
            :key="variant.id"
            class="color-dot"
            :style="{ backgroundColor: variant.hex }"
            :class="{ active: selectedVariant.id === variant.id }"
            @click="selectColor(variant)"
            :title="variant.color"
          ></button>
        </div>
      </div>

      <!-- အရေအတွက် ရွေးချယ်ရန်နေရာ -->
      <div class="option-section">
        <h3>Quantity</h3>
        <div class="quantity-selector">
          <button @click="quantity > 1 ? quantity-- : null" class="qty-btn">-</button>
          <span class="qty-number">{{ quantity }}</span>
          <button @click="quantity++" class="qty-btn">+</button>
        </div>
      </div>

      <!-- စုစုပေါင်းကျသင့်ငွေ ပြသခြင်းနှင့် Smart Buy Button -->
      <div class="action-section">
        <div class="total-price-display">
          <span class="total-label">Total Cost:</span>
          <span class="total-amount">${{ totalPrice }}</span>
        </div>
        
        <button class="buy-button" @click="handleBuy">
          🛒 Buy Now
        </button>
      </div>

    </div>
  </div>
</template>

<style scoped>
.product-container {
  display: flex;
  gap: 4rem;
  max-width: 1100px;
  margin: 80px auto;
  padding: 2rem;
  background: #ffffff;
  border-radius: 20px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.05);
  font-family: system-ui, -apple-system, sans-serif;
  color: #2d3748;
}

/* ဓာတ်ပုံ အပိုင်း CSS */
.image-gallery {
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
}

.main-image-wrapper {
  width: 100%;
  max-width: 400px;
  height: 450px;
  border-radius: 16px;
  overflow: hidden;
  background-color: #f7fafc;
  display: flex;
  justify-content: center;
  align-items: center;
}

.product-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.product-image:hover {
  transform: scale(1.05);
}

/* အသေးစိတ် အချက်အလက်များ အပိုင်း CSS */
.product-details {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.badge {
  background: #ebf8ff;
  color: #2b6cb0;
  font-size: 0.85rem;
  font-weight: 600;
  padding: 0.25rem 0.75rem;
  border-radius: 50px;
  width: fit-content;
  margin-bottom: 1rem;
}

.product-title {
  font-size: 2.5rem;
  font-weight: 800;
  margin: 0 0 1rem 0;
  color: #1a202c;
}

.product-description {
  color: #718096;
  line-height: 1.6;
  margin-bottom: 1.5rem;
}

.price-section {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 1.5rem;
}

.current-price {
  font-size: 2rem;
  font-weight: 700;
  color: #42b883;
}

.original-price {
  font-size: 1.25rem;
  color: #a0aec0;
  text-decoration: line-through;
}

.divider {
  border: 0;
  border-top: 1px solid #edf2f7;
  margin-bottom: 1.5rem;
}

.option-section {
  margin-bottom: 1.5rem;
}

.option-section h3 {
  font-size: 1rem;
  color: #4a5568;
  margin-bottom: 0.5rem;
}

.color-name {
  font-weight: 600;
  color: #2d3748;
}

/* Color Picker */
.color-picker {
  display: flex;
  gap: 1rem;
}

.color-dot {
  width: 32px;
  height: 32px;
  border-radius: 50%;
  border: 2px solid transparent;
  cursor: pointer;
  transition: transform 0.2s, border-color 0.2s;
  box-shadow: inset 0 2px 4px rgba(0,0,0,0.1);
}

.color-dot.active {
  border-color: #42b883;
  transform: scale(1.15);
}

/* Quantity Selector */
.quantity-selector {
  display: flex;
  align-items: center;
  background: #f7fafc;
  border-radius: 8px;
  width: fit-content;
  border: 1px solid #e2e8f0;
}

.qty-btn {
  background: transparent;
  border: none;
  width: 40px;
  height: 40px;
  font-size: 1.25rem;
  cursor: pointer;
  color: #4a5568;
  transition: background 0.2s;
}

.qty-btn:hover {
  background: #edf2f7;
}

.qty-number {
  width: 40px;
  text-align: center;
  font-weight: 600;
}

/* Cost & Buy Button Section */
.action-section {
  margin-top: auto;
  background: #f7fafc;
  padding: 1.5rem;
  border-radius: 12px;
  border: 1px solid #edf2f7;
}

.total-price-display {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1rem;
}

.total-label {
  font-size: 1.1rem;
  font-weight: 600;
  color: #4a5568;
}

.total-amount {
  font-size: 1.75rem;
  font-weight: 700;
  color: #2d3748;
}

.buy-button {
  width: 100%;
  background-color: #42b883;
  color: white;
  border: none;
  padding: 1rem;
  font-size: 1.2rem;
  font-weight: 700;
  border-radius: 8px;
  cursor: pointer;
  transition: background-color 0.2s, transform 0.1s;
  box-shadow: 0 4px 12px rgba(66, 184, 131, 0.3);
}

.buy-button:hover {
  background-color: #35495e;
}

.buy-button:active {
  transform: scale(0.98);
}

/* 📱 Responsive UI (ဖုန်းမျက်နှာပြင်အတွက် အလိုအလျောက် ပြောင်းလဲပေးမည့်စနစ်) */
@media (max-width: 768px) {
  .product-container {
    flex-direction: column;
    gap: 2rem;
    margin: 20px 10px;
    padding: 1rem;
  }

  .main-image-wrapper {
    height: 300px;
  }

  .product-title {
    font-size: 1.8rem;
  }
}
</style>