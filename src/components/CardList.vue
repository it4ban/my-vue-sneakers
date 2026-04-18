<script setup>
import CardItem from './CardItem.vue'

const onClickAdd = () => {
  alert('Добавить в корзину')
}

const onClickFavorite = () => {
  alert('Добавить в избранное')
}
</script>

<template>
  <div class="grid grid-cols-4 gap-5">
    <CardItem
      image-url="/sneakers/sneakers-1.jpg"
      title="Мужские Кроссовки Nike Blazer Mid Suede"
      :price="5000"
      :is-added="false"
      :is-favorite="false"
      @click-add="onClickAdd"
      @click-favorite="onClickFavorite"
    />
  </div>
</template>
