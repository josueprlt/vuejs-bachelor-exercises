<template>
  <div class="app-container">

    <div class="stats-row">
      <div class="stat-card">
        <span class="label">Prix Moyen</span>
        <span class="value">{{ formatCurrency(averageItemPrice) }}</span>
      </div>
      <div class="stat-card highlight">
        <span class="label">Économies</span>
        <span class="value">{{ formatCurrency(discountAmount) }}</span>
      </div>
    </div>

    <div class="main-grid">
      <div class="products-section">
        <h2>Catalogue</h2>
        <div class="product-list">
          <div
              v-for="product in products"
              :key="product.id"
              class="product-card"
              :style="{ borderLeftColor: product.color }"
          >
            <div class="prod-info">
              <h3>{{ product.name }}</h3>
              <p>{{ formatCurrency(product.price) }}</p>
            </div>
            <button
                @click="addToCart(product)"
                :disabled="product.stock <= 0"
                class="btn-add"
            >
              {{ product.stock > 0 ? 'Ajouter' : 'Rupture' }}
            </button>
          </div>
        </div>
      </div>

      <div class="cart-section card">
        <h2>Mon Panier ({{ itemCount }})</h2>

        <div v-if="alertMessage" class="alert-box">{{ alertMessage }}</div>

        <div v-if="cart.length > 0" class="cart-items">
          <div v-for="(item, index) in filteredItems" :key="item.id" class="cart-item">
            <span>{{ item.name }} (x{{ item.quantity }})</span>
            <div class="actions">
              <button @click="updateQuantity(item, -1)" class="btn-small">-</button>
              <button @click="updateQuantity(item, 1)" class="btn-small">+</button>
              <button @click="removeFromCart(item)" class="btn-small delete">×</button>
            </div>
            <span class="price">{{ formatCurrency(item.price * item.quantity) }}</span>
          </div>
          <p v-if="filteredItems.length === 0 && cart.length > 0" class="empty-text">Aucun résultat pour cette recherche.</p>
        </div>
        <p v-else class="empty-text">Votre panier est vide.</p>

        <button v-if="cart.length > 0" @click="clearCart" class="btn-text">Vider le panier</button>

        <hr>

        <div class="summary">
          <div class="row"><span>Sous-total:</span> <span>{{ formatCurrency(subtotal) }}</span></div>
          <div class="row"><span>Taxe ({{ taxRate }}%):</span> <span>{{ formatCurrency(tax) }}</span></div>
          <div class="row"><span>Livraison:</span> <span>{{ formatCurrency(shippingCost) }}</span></div>

          <div class="discount-section">
            <input
                v-model="discountCode"
                placeholder="Code promo (ex: SAVE10)"
                :class="{ 'valid': isDiscountValid, 'invalid': discountCode && !isDiscountValid }"
            >
            <small v-if="isDiscountValid" class="success-text">Code valide ! -{{ validDiscountCodes[discountCode] }}%</small>
            <small v-else-if="discountCode" class="error-text">Code invalide</small>
          </div>

          <div class="row discount" v-if="isDiscountValid">
            <span>Réduction:</span> <span>-{{ formatCurrency(discountAmount) }}</span>
          </div>

          <div class="row total">
            <span>Total:</span>
            <span>{{ formattedTotal }}</span>
          </div>
        </div>

        <button
            class="btn-checkout"
            :disabled="!isCheckoutEnabled"
        >
          Payer maintenant
        </button>

      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, watch } from 'vue'

const products = ref([
  { id: 1, name: 'Jus Detox', price: 100, color: '#42b883', stock: 10 },
  { id: 2, name: 'Jus Vitaminé', price: 200, color: '#f97316', stock: 5 },
  { id: 3, name: 'Smoothie Berry', price: 150, color: '#8b5cf6', stock: 8 }
]);

const cart = ref([]);

const taxRate = ref(20); // 20%
const discountCode = ref('');
const validDiscountCodes = ref({
  'WELCOME5': 5,
  'SAVE10': 10,
  'SPRING15': 15
});
const shippingCost = ref(10);
const searchQuery = ref('');
const alertMessage = ref('');

const formatCurrency = (value) => {
  return new Intl.NumberFormat('fr-FR', { style: 'currency', currency: 'EUR' }).format(value);
}

const subtotal = computed(() => {
  return cart.value.reduce((acc, item) => acc + (item.price * item.quantity), 0);
});

const tax = computed(() => {
  return subtotal.value * (taxRate.value / 100);
});

const itemCount = computed(() => {
  return cart.value.reduce((acc, item) => acc + item.quantity, 0);
});

const isDiscountValid = computed(() => {
  return Object.keys(validDiscountCodes.value).includes(discountCode.value);
});

const discountAmount = computed(() => {
  if (!isDiscountValid.value) return 0;
  const percentage = validDiscountCodes.value[discountCode.value];
  return subtotal.value * (percentage / 100);
});

const total = computed(() => {
  return subtotal.value + tax.value + shippingCost.value - discountAmount.value;
});

const averageItemPrice = computed(() => {
  if (itemCount.value === 0) return 0;
  return subtotal.value / itemCount.value;
});

const formattedTotal = computed(() => {
  return formatCurrency(total.value);
});

const filteredItems = computed(() => {
  if (!searchQuery.value) return cart.value;
  return cart.value.filter(item =>
      item.name.toLowerCase().includes(searchQuery.value.toLowerCase())
  );
});

const isCartEmpty = computed(() => cart.value.length === 0);

const isCheckoutEnabled = computed(() => {
  if (isCartEmpty.value) return false;
  return !(discountCode.value !== '' && !isDiscountValid.value);

});

function addToCart(product) {
  const existingItem = cart.value.find(item => item.id === product.id);

  if (existingItem) {
    existingItem.quantity++;
  } else {
    cart.value.push({ ...product, quantity: 1 });
  }
}

function removeFromCart(itemToRemove) {
  cart.value = cart.value.filter(item => item.id !== itemToRemove.id);
}

function updateQuantity(item, amount) {
  item.quantity += amount;
  if (item.quantity <= 0) {
    removeFromCart(item);
  }
}

function clearCart() {
  cart.value = [];
  discountCode.value = '';
}

watch(subtotal, (newVal) => {
  console.log(`Le sous-total a changé : ${newVal}€`);
});

watch(discountCode, (newVal) => {
  if (newVal === '') {
    alertMessage.value = '';
    return;
  }
  if (Object.keys(validDiscountCodes.value).includes(newVal)) {
    console.log("Code promo appliqué !");
  }
});

watch(cart, (newCart) => {
  console.log("Modification du panier détectée (Deep Watch)", newCart);
}, { deep: true });

</script>

<style scoped>
.app-container {
  max-width: 1000px;
  margin: 0 auto;
  padding: 2rem;
  font-family: 'Inter', sans-serif;
  background-color: #f8fafc;
  min-height: 100vh;
}

.stats-row {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1rem;
  margin-bottom: 2rem;
}

.stat-card {
  background: white;
  padding: 1rem;
  border-radius: 12px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.05);
  display: flex;
  flex-direction: column;
}

.stat-card.highlight { border-bottom: 3px solid #42b883; }

.label { font-size: 0.8rem; color: #64748b; text-transform: uppercase; letter-spacing: 0.5px; }
.value { font-size: 1.2rem; font-weight: 700; color: #1e293b; margin-top: 0.5rem; }

.main-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2rem;
}

.products-section, .cart-section {
  background: white;
  padding: 2rem;
  border-radius: 16px;
  box-shadow: 0 4px 6px -1px rgba(0,0,0,0.05);
}

.card h2 { margin-top: 0; color: #334155; }

.product-card {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem;
  border: 1px solid #e2e8f0;
  margin-bottom: 1rem;
  border-radius: 8px;
  border-left: 4px solid #ccc;
  transition: transform 0.2s;
}
.product-card:hover { transform: translateX(5px); }
.prod-info h3 { margin: 0 0 0.25rem 0; font-size: 1rem; }
.prod-info p { margin: 0; color: #64748b; font-weight: 600; }

.btn-add {
  background: #1e293b;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 6px;
  cursor: pointer;
}
.btn-add:disabled { background: #cbd5e1; cursor: not-allowed; }

.search-input {
  width: 100%;
  padding: 10px;
  border: 1px solid #e2e8f0;
  border-radius: 8px;
  margin-bottom: 1rem;
  box-sizing: border-box;
}

.cart-items { margin-bottom: 1.5rem; }
.cart-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.5rem 0;
  border-bottom: 1px dashed #e2e8f0;
}
.actions { display: flex; gap: 5px; }
.btn-small {
  border: 1px solid #cbd5e1;
  background: transparent;
  width: 24px;
  height: 24px;
  border-radius: 4px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
}
.btn-small.delete { color: #ef4444; border-color: #fca5a5; }

.summary .row {
  display: flex;
  justify-content: space-between;
  margin-bottom: 0.5rem;
  color: #475569;
}
.summary .total {
  font-size: 1.25rem;
  font-weight: 800;
  color: #1e293b;
  margin-top: 1rem;
  padding-top: 1rem;
  border-top: 2px solid #f1f5f9;
}
.summary .discount { color: #166534; font-weight: 600; }

.discount-section { margin: 1rem 0; }
.discount-section input {
  width: 100%;
  padding: 8px;
  border: 1px solid #e2e8f0;
  border-radius: 6px;
  box-sizing: border-box;
}
.discount-section input.valid { border-color: #42b883; background: #f0fdf4; }
.discount-section input.invalid { border-color: #ef4444; background: #fef2f2; }

.success-text { color: #166534; display: block; margin-top: 4px; }
.error-text { color: #991b1b; display: block; margin-top: 4px; }

.alert-box {
  background: #fff7ed;
  color: #c2410c;
  padding: 0.75rem;
  border-radius: 8px;
  margin-bottom: 1rem;
  font-size: 0.9rem;
  border: 1px solid #ffedd5;
}

.delivery-info {
  margin-top: 1rem;
  font-size: 0.85rem;
  color: #64748b;
  text-align: center;
  background: #f8fafc;
  padding: 8px;
  border-radius: 6px;
}

.btn-checkout {
  width: 100%;
  padding: 1rem;
  background: #42b883;
  color: white;
  border: none;
  font-weight: 700;
  border-radius: 8px;
  font-size: 1rem;
  margin-top: 1.5rem;
  cursor: pointer;
  transition: background 0.2s;
}
.btn-checkout:disabled { background: #cbd5e1; cursor: not-allowed; }
.btn-checkout:hover:not(:disabled) { background: #3aa876; }
.btn-text { background: none; border: none; color: #64748b; text-decoration: underline; cursor: pointer; font-size: 0.8rem; }
.empty-text { text-align: center; color: #94a3b8; font-style: italic; }
</style>