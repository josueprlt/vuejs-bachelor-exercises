<template>
  <div class="app-container">

    <div class="products-grid">
      <div
          class="product-card"
          v-for="product in products"
          :key="product.id"
          :style="{ borderTopColor: product.color }"
      >
        <div class="image-container">
          <img :src="product.image" :alt="product.name">
        </div>

        <div class="card-content">
          <header>
            <h1>{{ product.name }}</h1>
            <span class="price">{{ product.price }} €</span>
          </header>

          <p class="description">{{ product.description }}</p>

          <div class="meta">
            <span
                class="stock-badge"
                :class="{ 'out-of-stock': product.stock <= 0 }"
            >
              <span class="dot"></span>
              {{ product.stock <= 0 ? 'Out of stock' : `${product.stock} en stock` }}
            </span>
          </div>

          <button class="add-btn">Add to cart</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const products = ref([
  {
    id: 1,
    name: 'Jus Detox',
    price: 100,
    color: '#42b883',
    description: 'Une cure de jouvence naturelle pour votre corps.',
    stock: 10,
    image: 'https://marketplace.canva.com/EAGTHgKgAkQ/2/0/1131w/canva-affiche-promotion-de-produit-moderne-vert-et-blanc-rP6hxxPRVLQ.jpg'
  },
  {
    id: 2,
    name: 'Jus Vitaminé',
    price: 200,
    color: '#f97316',
    description: 'Le plein d\'énergie pour affronter la journée.',
    stock: 0,
    image: 'https://img.freepik.com/psd-gratuit/modele-affiche-jus-biologique_23-2148911054.jpg?semt=ais_hybrid&w=740&q=80'
  }
]);
</script>

<style scoped>
.app-container {
  background-color: #f0f4f8;
  font-family: 'Inter', -apple-system, sans-serif;
  padding: 3rem;
  display: flex;
  gap: 2rem;
  align-items: flex-start;
  justify-content: center;
  flex-wrap: wrap;
}

.products-grid {
  display: flex;
  gap: 2rem;
  flex-wrap: wrap;
}

.product-card {
  background: white;
  border-radius: 16px;
  width: 320px;
  overflow: hidden;
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.05);
  transition: transform 0.2s ease, box-shadow 0.2s ease;

  border-top: 4px solid transparent;
  display: flex;
  flex-direction: column;
}

.product-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
}

.image-container {
  height: 200px;
  width: 100%;
  overflow: hidden;
}

img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s ease;
}

.product-card:hover img {
  transform: scale(1.05);
}

.card-content {
  padding: 1.5rem;
  display: flex;
  flex-direction: column;
  flex-grow: 1;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 0.5rem;
}

h1 {
  font-size: 1.25rem;
  color: #1e293b;
  margin: 0;
  font-weight: 700;
}

.price {
  font-weight: 700;
  color: #334155;
  font-size: 1.1rem;
  background: #f1f5f9;
  padding: 4px 8px;
  border-radius: 6px;
}

.description {
  color: #64748b;
  font-size: 0.9rem;
  line-height: 1.5;
  margin-bottom: 1.5rem;
}

.meta {
  margin-bottom: 1.5rem;
}

.stock-badge {
  display: inline-flex;
  align-items: center;
  font-size: 0.75rem;
  font-weight: 600;
  color: #166534;
  background: #dcfce7;
  padding: 4px 10px;
  border-radius: 99px;
}

.dot {
  width: 6px;
  height: 6px;
  background-color: currentColor;
  border-radius: 50%;
  margin-right: 6px;
}

.stock-badge.out-of-stock {
  color: #991b1b;
  background: #fee2e2;
}

.add-btn {
  margin-top: auto;
  width: 100%;
  padding: 0.8rem;
  border: none;
  background-color: #1e293b;
  color: white;
  font-weight: 600;
  border-radius: 8px;
  cursor: pointer;
  transition: background 0.2s;
}

.add-btn:hover {
  background-color: #42b883;
}
</style>