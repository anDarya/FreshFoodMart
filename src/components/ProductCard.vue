<template>
  <div class="border p-4 rounded-lg shadow-lg bg-green-50">
    <img :src="product.image" alt="Product Image" class="product-image w-full h-72 object-cover mb-4">
    <h2 class="text-xl font-bold mb-2">{{ product.title }}</h2>
    <p class="text-lime-600 text-xl font-bold mb-2">${{ product.price.toFixed(2) }}</p>
    <div class="mb-2">
      <Stars :rating="product.rating" />
    </div>
    <div class="flex justify-center items-center mb-2">
      <img :src="product.manufacturer" alt="Manufacturer" class="w-7 h-6">
      <p class="text-gray-500 text-lg ml-4">Remaining {{ product.stock }}</p>
    </div>
    <div class="flex items-center space-x-2 justify-center mb-2">
      <button 
        @click="decrement" 
        class="p-2 bg-transparent rounded-lg hover:bg-green-100 hover:border-green-100 focus:outline-none"
      >
        <img src="./../assets/icons/minus.svg" alt="Decrease" class="w-7 h-6"> 
      </button>
      <input
        type="number"
        :value="quantity"
        readonly
        class="w-12 pl-3.5 text-center border border-gray-300 rounded py-1 bg-white"
      />
      <button 
        @click="increment" 
        class="p-2 bg-transparent rounded-lg hover:bg-green-100 hover:border-green-100 focus:outline-none"
      >
        <img src="./../assets/icons/plus.svg" alt="Increase" class="w-7 h-6"> 
      </button>
    </div>
    <button 
      @click="addToCart" 
      class="bg-[#688b23] text-white p-2 rounded w-1/2 focus:outline-none"
    >
      Add to Cart
    </button>
  </div>
</template>

<script>
import { ref } from 'vue'
import Stars from './Raiting.vue'

export default {
  props: {
    product: Object
  },
  components: {
    Stars
  },
  setup(props, { emit }) {
    const quantity = ref(1);

    const addToCart = () => {
      if (quantity.value > 0 && quantity.value <= props.product.stock) {
        emit('add-to-cart', props.product, quantity.value);
      }
    };

    const increment = () => {
      if (quantity.value < props.product.stock) {
        quantity.value += 1;
      }
    };

    const decrement = () => {
      if (quantity.value > 1) {
        quantity.value -= 1;
      }
    };

    return { quantity, addToCart, increment, decrement };
  }
}
</script>

<style scoped>
.product-image {  
  background-size: cover;
  background-position: center;
}
</style>