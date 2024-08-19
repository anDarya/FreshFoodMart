<template>
  <div class="flex items-center justify-center space-x-1">
    <template v-for="index in 5">
      <svg
        v-if="index <= filledStars"
        xmlns="http://www.w3.org/2000/svg"
        class="h-6 w-6 text-yellow-400"
        viewBox="0 0 24 24"
        fill="currentColor"
        :key="'filled-' + index"
      >
        <path d="M12 2l2.356 6.782 7.145.518-5.118 4.383 1.941 7.317-6.334-4.53-6.333 4.53 1.941-7.317-5.118-4.383 7.145-.518L12 2z" />
      </svg>
      <svg
        v-else-if="index <= totalStars"
        xmlns="http://www.w3.org/2000/svg"
        class="h-6 w-6 text-yellow-400 border border-yellow-400"
        viewBox="0 0 24 24"
        fill="none"
        :key="'border-' + index"
      >
        <path d="M12 2l2.356 6.782 7.145.518-5.118 4.383 1.941 7.317-6.334-4.53-6.333 4.53 1.941-7.317-5.118-4.383 7.145-.518L12 2z" />
      </svg>
    </template>
  </div>
</template>

<script>
export default {
  name: 'Stars',
  props: {
    rating: {
      type: Number,
      required: true,
      validator(value) {
        return value >= 1 && value <= 5;
      }
    }
  },
  computed: {
    filledStars() {
      return Math.floor(this.rating);
    },
    totalStars() {
      return this.rating;
    }
  }
};
</script>