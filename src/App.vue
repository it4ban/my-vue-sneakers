<script setup>
import AppHeader from './components/AppHeader.vue'
import CardList from './components/CardList.vue'
import DrawerCart from './components/DrawerCart.vue'
</script>

<template>
  <!-- <DrawerCart /> -->

  <div class="w-4/5 mx-auto bg-white rounded-xl shadow-xl mt-14">
    <AppHeader />

    <div class="p-10">
      <div class="flex justify-between items-center">
        <h1 class="text-3xl font-bold mb-10">Все кроссовки</h1>

        <div class="flex gap-4">
          <select class="py-2 px-3 border rounded-md outline-none border-slate-200">
            <option>По названию</option>
            <option>По цене (дешевые)</option>
            <option>По цене (дорогие)</option>
          </select>

          <div class="relative">
            <img class="absolute left-4 top-3" src="/search.svg" alt="Search" />

            <input
              class="border border-slate-200 rounded-md py-2 pl-11 pr-4 outline-none focus:border-gray-400"
              placeholder="Поиск..."
              type="text"
            />
          </div>
        </div>
      </div>

      <CardList />
    </div>
  </div>
</template>
