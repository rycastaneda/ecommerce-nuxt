<template>
  <div>
    <ProductDetails :product="product" :on-cart-add="onCartAdd"/>
  </div>
</template>

<script setup>
  import { useStorage } from '@vueuse/core'
  const { id } = useRoute().params
  const uri = 'https://fakestoreapi.com/products/' + id

  const  cartItems = useStorage('cartItems', [], undefined, {
    serializer: {
      read: (v) => v ? JSON.parse(v) : null,
      write: (v) => JSON.stringify(v),
    },
  })
  console.log('cartItems', cartItems);
  //  fetch the products
  const { data: product } = await useFetch(uri, { key: id })

  product.value.inCart =  Boolean(cartItems.value.find(item => item.id === product.value.id))

  if (!product.value) {
    throw createError({ statusCode: 404, statusMessage: 'Product not found' })
  }

  console.log('product', product.value);

  function onCartAdd(item) {
    console.log('item', item);
    
    cartItems.value.push(item);
    // setCartItems(cartItems)
  }

  definePageMeta({
    layout: "default",
  })
</script>