<script setup>
import CardItem from './CardItem.vue'
</script>

<template>
  <div class="grid grid-cols-4 gap-5">
    <CardItem
      image-url="/sneakers/sneakers-1.jpg"
      title="Мужские Кроссовки Nike Blazer Mid Suede"
      :price="5000"
    />
    <CardItem />
    <CardItem />
    <CardItem />
    <CardItem />
    <CardItem />
    <CardItem />
    <CardItem />
    <CardItem />
  </div>
</template>
