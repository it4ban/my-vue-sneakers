<script setup>
import CardItem from './CardItem.vue'

defineProps({
  items: Array,
})

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
      v-for="item in items"
      :key="item.id"
      :title="item.title"
      :image-url="item.imageUrl"
      :price="item.price"
      :is-added="false"
      :is-favorite="false"
      @click-add="onClickAdd"
      @click-favorite="onClickFavorite"
    />
  </div>
</template>
