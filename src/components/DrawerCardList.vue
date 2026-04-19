<script setup>
import { inject } from 'vue'
import DrawerCard from './DrawerCard.vue'

const { cart, addToCart, removeFromCart } = inject('card')
</script>

<template>
  <div class="flex flex-col gap-4 justify-between">
    <DrawerCard
      v-for="item in cart"
      :key="item.id"
      :title="item.title"
      :price="item.price"
      :image-url="item.imageUrl"
      @on-click-remove="removeFromCart(item)"
    />
  </div>
</template>
