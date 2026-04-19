<script setup>
import CardItem from './CardItem.vue'

defineProps({
  items: Array,
})

const emit = defineEmits(['addToFavorite'])

const onClickAdd = () => {
  alert('Добавить в корзину')
}
</script>

<template>
  <div class="grid grid-cols-4 gap-5">
    <CardItem
      v-for="item in items"
      :key="item.id"
      :id="item.id"
      :title="item.title"
      :image-url="item.imageUrl"
      :price="item.price"
      :is-added="item.isAdded"
      :is-favorite="item.isFavorite"
      @click-add="onClickAdd"
      @click-favorite="emit('addToFavorite', item)"
    />
  </div>
</template>
