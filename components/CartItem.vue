<template>
    <section role="cart-item" class="flex items-center relative font-bold mb-2">
      <div class="w-48">
        <img :src="product.image" class="aspect-square rounded w-full h-24" alt="" />
      </div>
      <div class="w-full pl-6">
        <h2>{{product.title}}</h2>
        <p><span class="text-gray">${{ product.price }}</span> </p>
      </div>
      <div class="w-48 text-center">
        <button class="btn" @click="onCartRemove(product.id)">
          Remove
        </button>
      </div>
    </section>
  </template>
  
  <script setup>
    const { product } = defineProps(['product', 'onCartRemove'])
  </script>
  
  <style scoped>
    img {
      max-width: 400px;
    }
  </style>