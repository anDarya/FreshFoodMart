<template>
  <div class="flex flex-col min-h-screen">
    <Header @toggle-cart="toggleCart" />
    <CartModal :showModal="showModal" @close-modal="toggleCart" />
    <main class="flex-grow">
      <HomePage />
      <ProductList />
    </main>
    <Footer />
  </div>
</template>

<script>
import Header from './components/Header.vue'
import CartModal from './components/CartModal.vue'
import HomePage from './components/HomePage.vue'
import ProductList from './components/ProductList.vue'
import Footer from './components/Footer.vue'
import { ref } from 'vue'

export default {
  components: {
    Header,
    CartModal,
    HomePage,
    ProductList,
    Footer
  },
  
  setup() {    
    const showModal = ref(false);

    const toggleCart = () => {
      showModal.value = !showModal.value;
    };

    return { showModal, toggleCart };
  }
}
</script>