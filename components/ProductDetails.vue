<template>
  <div class="card">
    <div class="grid grid-cols-2 gap-10">
      <div class="p-7">
        <img :src="`${refProduct.image}`" class="mx-auto my-7" />
      </div>
      <div class="p-7">
        <h2 class="text-4xl my-7">{{ refProduct.title }}</h2>
        <p class="text-xl my-7">Price - ${{ refProduct.price }}</p>
        <h3 class="font-bold border-b-2 mb-4 pb-2">Product description:</h3>
        <p class="mb-7">{{ refProduct.description }}</p>
        <button class="btn" :disabled="refProduct.inCart" @click="onCartAdd(refProduct)">Add to Cart</button>
      </div>
    </div>
  </div>
</template>

<script setup>
  const { product } = defineProps(['product', 'onCartAdd'])
  const refProduct = ref(product)
</script>

<style scoped>
  img {
    max-width: 400px;
  }
</style>