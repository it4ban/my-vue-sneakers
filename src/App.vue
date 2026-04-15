<script setup>
import AppHeader from './components/AppHeader.vue'
import CardList from './components/CardList.vue'
</script>

<template>
  <div class="w-4/5 mx-auto bg-white rounded-xl shadow-xl mt-14">
    <AppHeader />

    <div class="p-10">
      <h1 class="text-3xl font-bold mb-10">Все кроссовки</h1>

      <CardList />
    </div>
  </div>
</template>
