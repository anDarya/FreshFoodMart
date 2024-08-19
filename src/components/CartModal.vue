<template>
  <div v-if="showModal" class="fixed inset-0 flex items-center justify-center bg-gray-900 bg-opacity-50 h-full overflow-y-auto">
    <div class="bg-white p-4 rounded-lg modal-content w-full max-w-md overflow-y-auto">
      <div v-if="cartProducts.length === 0" class="text-center text-gray-600">
        Lista este goală
      </div>
      <div v-for="item in cartProducts" :key="item.id" class="mb-4 border-b pb-4">
        <img :src="item.image" alt="Product Image" class="w-full h-32 object-cover mb-4">
        <h2 class="text-xl font-bold mb-2">{{ item.title }}</h2>
        <p class="text-lime-600 text-xl font-bold mb-2">$ {{ item.price }}</p>
        <div class="flex justify-center items-center mb-2">
          <img :src="item.manufacturer" alt="Manufacturer" class="w-7 h-6">
          <p class="text-gray-500 text-lg ml-4">Remaining {{ item.stock }}</p>
        </div>
        <div class="flex items-center mt-2 justify-center">
          <button @click="decrementQuantity(item)" class="p-2 bg-transparent rounded-lg hover:bg-green-100 hover:border-green-100 focus:outline-none">
            <img src="./../assets/icons/minus.svg" alt="Decrease" class="w-7 h-6">
          </button>
          <input type="number" :value="item.quantity" readonly class="w-12 pl-3.5 text-center border border-gray-300 rounded py-1 bg-white">
          <button @click="incrementQuantity(item)" class="p-2 bg-transparent rounded-lg hover:bg-green-100 hover:border-green-100 focus:outline-none">
            <img src="./../assets/icons/plus.svg" alt="Increase" class="w-7 h-6">
          </button>
        </div>
        <button @click="removeFromCart(item.id)" class="mt-4 px-4 py-2 bg-red-500 text-white rounded">Remove from Cart</button>
      </div>
      <div class="font-bold mt-4">Total: ${{ totalPriceFormatted }}</div>
      <button @click="closeModal" class="mt-2 px-4 py-2 bg-gray-300 rounded">Close</button>
    </div>
  </div>
</template>

<script>
import { ref, computed, watch } from 'vue';

export default {
  props: {
    showModal: Boolean
  },
  setup(props, { emit }) {
    const cartProducts = ref([]);

    const updateCartProducts = () => {
      cartProducts.value = JSON.parse(localStorage.getItem('cart')) || [];
    };

    const totalPrice = computed(() => {
      return cartProducts.value.reduce((sum, item) => sum + (item.price * (item.quantity || 1)), 0);
    });

    const totalPriceFormatted = computed(() => totalPrice.value.toFixed(2));

    const incrementQuantity = (item) => {
      item.quantity += 1;
      saveCart();
    };

    const decrementQuantity = (item) => {
      if (item.quantity > 1) {
        item.quantity -= 1;
        saveCart();
      }
    };

    const removeFromCart = (productId) => {
      cartProducts.value = cartProducts.value.filter(item => item.id !== productId);
      saveCart();
    };

    const saveCart = () => {
      localStorage.setItem('cart', JSON.stringify(cartProducts.value));
      window.dispatchEvent(new Event('cart-updated'));
    };

    const closeModal = () => {
      emit('close-modal');
    };

    watch(() => props.showModal, (newVal) => {
      if (newVal) {
        updateCartProducts();
      }
    });

    return { cartProducts, totalPriceFormatted, incrementQuantity, decrementQuantity, removeFromCart, closeModal };
  }
};
</script>

<style scoped>
.modal-content {
  max-height: calc(100vh - 150px);
  overflow-y: auto;
}

@media (max-width: 640px) {
  .modal-content {
    max-width: 90%;
  }
}

@media (min-width: 641px) and (max-width: 768px) {
  .modal-content {
    max-width: 80%;
  }
}

@media (min-width: 769px) {
  .modal-content {
    max-width: 40%;
  }
}
</style>