<template>
  <div>
    <header class="shadow-sm bg-white">
      <nav class="container mx-auto p-4 flex justify-between">
        <NuxtLink to="/" class="font-bold">Ecommerce</NuxtLink>
        <ul class="relative flex items-center gap-4">
          <li><NuxtLink to="/">Home</NuxtLink></li>
          <li><NuxtLink to="/about">About</NuxtLink></li>
          <li><NuxtLink to="/products">Products</NuxtLink></li>
          <li>
            <button @click="toggleModal" class="flex items-center">
              <svg class="w-4 h-4 text-white" focusable="false" aria-hidden="true" viewBox="0 0 24 24" data-testid="ShoppingCartIcon"><path d="M7 18c-1.1 0-1.99.9-1.99 2S5.9 22 7 22s2-.9 2-2-.9-2-2-2zM1 2v2h2l3.6 7.59-1.35 2.45c-.16.28-.25.61-.25.96 0 1.1.9 2 2 2h12v-2H7.42c-.14 0-.25-.11-.25-.25l.03-.12.9-1.63h7.45c.75 0 1.41-.41 1.75-1.03l3.58-6.49c.08-.14.12-.31.12-.48 0-.55-.45-1-1-1H5.21l-.94-2H1zm16 16c-1.1 0-1.99.9-1.99 2s.89 2 1.99 2 2-.9 2-2-.9-2-2-2z"></path></svg>
              {{ cartItems.length }}
            </button>
          </li>
          <Popup :isOpen="isModalOpened" @modal-close="closeModal" @submit="submitHandler" name="first-modal">
            <h4 v-if="!cartItems.length">No Items at the moment</h4>
            <CartItem v-for="item in cartItems" :product="item" :on-cart-remove="onRemove"/>
          </Popup>
        </ul>
      </nav>
    </header>
    <div class="container mx-auto p-4">
      <slot />
    </div>
  </div>
</template>

<script setup>
  import { useStorage } from '@vueuse/core'
  const  cartItems = useStorage('cartItems', [], undefined, {
    serializer: {
      read: (v) => v ? JSON.parse(v) : null,
      write: (v) => JSON.stringify(v),
    },
  })
  const isModalOpened = ref(false)

  function closeModal() {
    isModalOpened.value = false
  }
  function toggleModal() {
    isModalOpened.value = !isModalOpened.value
  }

  function onRemove(id) {
    console.log('id', id);
    cartItems.value = cartItems.value.filter(item => item.id !== id)
  }
</script>

<style scoped>
  .router-link-exact-active {
    color: #12b488;
  }
</style>