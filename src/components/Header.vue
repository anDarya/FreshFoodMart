<template>
  <header class="bg-[#cedada] text-blue p-4 flex justify-between items-center sticky top-0 z-50">
    <div class="flex items-center pl-3">
      <img src="./../assets/logo.svg" alt="Vue logo" />
      <div class="text-xl font-bold text-[#688b23] ml-2">Logo</div>
    </div>
    <div @click="handleToggleCart" class="relative cursor-pointer">
      <img src="./../assets/cart.svg" alt="Cart" />
      <span v-if="cartItemCount > 0" class="absolute top-0 right-0 bg-red-700 text-white text-xs font-bold rounded-full px-1 pb-0.5">
        {{ cartItemCount }}
      </span>
    </div>
  </header>
</template>

<script>
import { ref, onMounted, onUnmounted } from 'vue';

export default {
  emits: ['toggle-cart'],
  setup(props, { emit }) {
    const cartItemCount = ref(0);

    const updateCartCount = () => {
      const cart = JSON.parse(localStorage.getItem('cart')) || [];
      cartItemCount.value = cart.length;
    };

    onMounted(() => {
      updateCartCount();
      window.addEventListener('cart-updated', updateCartCount);
    });

    onUnmounted(() => {
      window.removeEventListener('cart-updated', updateCartCount);
    });

    const handleToggleCart = () => {
      if (cartItemCount.value > 0) {
        emit('toggle-cart');
      }
    };

    return { cartItemCount, handleToggleCart };
  }
};
</script>