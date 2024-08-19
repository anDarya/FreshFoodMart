<template>
  <div class="p-4 grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4">
    <ProductCard
      v-for="product in products"
      :key="product.id"
      :product="product"
      @add-to-cart="handleAddToCart"
    />
  </div>
</template>


<script>
import ProductCard from './ProductCard.vue';
import { ref } from 'vue';

export default {
  components: {
    ProductCard
  },
  setup() {
    const products = ref([
      {
        id: 1,
        image: '/src/assets/products/apple.jpg',
        title: 'Apple',
        price: 10.0,
        rating: 4,
        manufacturer: '/src/assets/flags/md.svg',
        stock: 20
      },
      {
        id: 2,
        image: '/src/assets/products/brocoli.jpg',
        title: 'Broccoli',
        price: 15.0,
        rating: 5,
        manufacturer: '/src/assets/flags/ro.svg',
        stock: 5
      },
      {
        id: 3,
        image: '/src/assets/products/cucumber.jpg',
        title: 'Cucumber',
        price: 10.0,
        rating: 3,
        manufacturer: '/src/assets/flags/ukr.svg',
        stock: 20
      },
      {
        id: 4,
        image: '/src/assets/products/grape.jpg',
        title: 'Grapes',
        price: 15.0,
        rating: 2,
        manufacturer: '/src/assets/flags/ger.svg',
        stock: 7
      },
      {
        id: 5,
        image: '/src/assets/products/potatoes.png',
        title: 'Potatoes',
        price: 10.0,
        rating: 1,
        manufacturer: '/src/assets/flags/md.svg',
        stock: 10
      },
      {
        id: 6,
        image: '/src/assets/products/tomatoes.jpg',
        title: 'Tomatoes',
        price: 15.0,
        rating: 3,
        manufacturer: '/src/assets/flags/ukr.svg',
        stock: 1
      }
    ]);

    const cart = ref([]);

    const loadCart = () => {
      cart.value = JSON.parse(localStorage.getItem('cart')) || [];
    };

    const saveCart = () => {
      localStorage.setItem('cart', JSON.stringify(cart.value));
      window.dispatchEvent(new Event('cart-updated'));
    };

    const handleAddToCart = (product, quantity) => {
      loadCart();
      const existingProduct = cart.value.find(item => item.id === product.id);
      if (existingProduct) {
        existingProduct.quantity = quantity;
      } else {
        cart.value.push({ ...product, quantity });
      }
      saveCart();
    };

    return { products, handleAddToCart };
  }
};
</script>