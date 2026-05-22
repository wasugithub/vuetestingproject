<script setup>
import {ref,computed} from 'vue'

const searchQuery =ref('')

const products =ref([
    { id: 1, name: 'VuePhone 15 Pro', price: 999, tag: 'Trending', image: 'https://images.unsplash.com/photo-1695048133142-1a20484d2569?w=500&auto=format&fit=crop&q=60' },
  { id: 2, name: 'VuePhone 15 Ultra', price: 1199, tag: 'Best Choice', image: 'https://images.unsplash.com/photo-1616348436168-de43ad0db179?w=500&auto=format&fit=crop&q=60' },
  { id: 3, name: 'VuePhone 15 Mini', price: 699, tag: 'Budget King', image: 'https://images.unsplash.com/photo-1510557880182-3d4d3cba35a5?w=500&auto=format&fit=crop&q=60' },
  { id: 4, name: 'VueBook Air', price: 1299, tag: 'New', image: 'https://images.unsplash.com/photo-1517336714731-489689fd1ca8?w=500&auto=format&fit=crop&q=60' },
  { id: 5, name: 'VueWatch Series 9', price: 399, tag: 'Hot', image: 'https://images.unsplash.com/photo-1508685096489-7aacd43bd3b1?w=500&auto=format&fit=crop&q=60' }
])

const filteredProducts = computed(() => {
    if(!searchQuery.value){
        return products.value
    }

    const query = searchQuery.value.toLowerCase().trim()
    return products.value.filter(product => {
        return product.name.toLowerCase().includes(query)
    })
})

const clearSearch = () => {
    searchQuery.value = ''
}
</script>

<template>
    <div class="search-section">

        <div class="search-box-container">
            <div class="search-input-wrapper">
                <span class="search-icon">🔍</span>
                <input v-model="searchQuery" type="text" placeholder="Type to search (e.g.. pro , mini, watch)... " class="search-input">
                <button v-if="searchQuery" @click="clearSearch" class="clear-btn">✕</button>
            </div>

          <p class="search-status" v-if="searchQuery">
            Found {{ filteredProducts.length }} products for "{{ searchQuery }}"   <!--ask the question -->
          </p>
        </div>

        <div class="product-grid" v-if="filteredProducts.length > 0">
            <div v-for="product in filteredProducts" :key="product.id" class="product-card">
                <div class="image-wrapper">
                    <span class="product-tag">{{ product.tag }}</span>
                    <img :src="product.image" :alt="product.name" class="product-img">
                </div>
                <div class="card-body">
                    <h3 class="product-name">{{ product.name }}</h3>
                    <p class="product-price">{{ product.price }}</p>
                    <button class="view-btn">view Detail</button>
                </div>
            </div>
        </div>

        <div class="no-results" v-else>
            <div class="no-results-icon">🕵️‍♂️</div>
            <h3>No Products Found</h3>
      <p>သင်ရှာဖွေနေတဲ့ နာမည်နဲ့ ကိုက်ညီတဲ့ ကုန်ပစ္စည်း မရှိပါဘူး။ တခြားနာမည်တစ်ခုခု ပြောင်းရိုက်ကြည့်ပါ။</p>
        </div>


    </div>
</template>

<style scoped>

.search-section {
  max-width: 1200px;
  width: 100%;
  margin: 0 auto;
  padding: 2rem;
  font-family: system-ui, -apple-system, sans-serif;
}

/* Search Box CSS */
.search-box-container {
  max-width: 600px;
  margin:  3rem auto;
  text-align: center;
}

.search-input-wrapper {
  position: relative;
  display: flex;
  align-items: center;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.05);
  border-radius: 50px;
  background: white;
  border: 2px solid #edf2f7;
  transition: border-color 0.2s, box-shadow 0.2s;
}

.search-input-wrapper:focus-within {
  border-color: #42b883;
  box-shadow: 0 4px 20px rgba(66, 184, 131, 0.15);
}

.search-icon {
  padding-left: 1.5rem;
  font-size: 1.2rem;
}

.search-input {
  width: 100%;
  padding: 1rem 1rem 1rem 0.75rem;
  border: none;
  background: transparent;
  font-size: 1.1rem;
  color: #2d3748;
  outline: none;
}

.clear-btn {
  background: none;
  border: none;
  padding-right: 1.5rem;
  font-size: 1rem;
  cursor: pointer;
  color: #a0aec0;
}

.clear-btn:hover {
  color: #e53e3e;
}

.search-status {
  margin-top: 0.75rem;
  font-size: 0.9rem;
  color: #718096;
}

/* Product Grid (1 Row, 3 Products) */
.product-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
}

.product-card {
  background: #ffffff;
  border-radius: 16px;
  overflow: hidden;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.05);
  display: flex;
  flex-direction: column;
  transition: transform 0.3s;
}

.product-card:hover {
  transform: translateY(-5px);
}

.image-wrapper {
  position: relative;
  height: 220px;
  background: #f7fafc;
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
  background: #35495e;
  color: white;
  font-size: 0.75rem;
  font-weight: 700;
  padding: 0.25rem 0.75rem;
  border-radius: 50px;
}

.card-body {
  padding: 1.5rem;
  display: flex;
  flex-direction: column;
  flex-grow: 1;
}

.product-name {
  font-size: 1.2rem;
  color: #2d3748;
  margin-bottom: 0.5rem;
}

.product-price {
  font-size: 1.3rem;
  color: #42b883;
  font-weight: 700;
  margin-bottom: 1rem;
}

.view-btn {
  margin-top: auto;
  background-color: #42b883;
  color: white;
  border: none;
  padding: 0.75rem;
  font-weight: 600;
  border-radius: 8px;
  cursor: pointer;
  transition: background-color 0.2s;
}

.view-btn:hover {
  background-color: #35495e;
}

/* No Results UI */
.no-results {
  text-align: center;
  padding: 4rem 2rem;
  background: white;
  border-radius: 16px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.05);
  max-width: 500px;
  margin: 0 auto;
}

.no-results-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
}

.no-results h3 {
  color: #2d3748;
  margin-bottom: 0.5rem;
}

.no-results p {
  color: #718096;
  font-size: 0.95rem;
  line-height: 1.5;
}

/* Responsive UI */
@media (max-width: 900px) {
  .product-grid { grid-template-columns: repeat(2, 1fr); }
}
@media (max-width: 600px) {
  .product-grid { grid-template-columns: 1fr; }
}

</style>