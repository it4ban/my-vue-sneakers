<script setup>
import { onMounted, reactive, ref, watch } from 'vue'
import axios from 'axios'

import AppHeader from './components/AppHeader.vue'
import CardList from './components/CardList.vue'
import DrawerCart from './components/DrawerCart.vue'

const items = ref([])

const filters = reactive({
  sortBy: 'title',
  searchQuery: '',
})

const onChangeSelect = (event) => {
  filters.sortBy = event.target.value
}

const onChangeSearchInput = (event) => {
  filters.searchQuery = event.target.value
}

const fetchItems = async () => {
  try {
    const params = {
      sortBy: filters.sortBy,
    }

    if (filters.searchQuery) {
      params.title = `*${filters.searchQuery}*`
    }

    const { data } = await axios.get('https://cca5a6a137f3ca08.mokky.dev/items', {
      params,
    })

    items.value = data
  } catch (err) {
    console.error('Error fetching items:', err)
  }
}

onMounted(fetchItems)
watch(filters, fetchItems)
</script>

<template>
  <!-- <DrawerCart /> -->

  <div class="w-4/5 mx-auto bg-white rounded-xl shadow-xl my-14">
    <AppHeader />

    <div class="p-10">
      <div class="flex justify-between items-center">
        <h1 class="text-3xl font-bold mb-10">Все кроссовки</h1>

        <div class="flex gap-4">
          <select
            @change="onChangeSelect"
            class="py-2 px-3 border rounded-md outline-none border-slate-200"
          >
            <option value="title">По названию</option>
            <option value="price">По цене (дешевые)</option>
            <option value="-price">По цене (дорогие)</option>
          </select>

          <div class="relative">
            <img class="absolute left-4 top-3" src="/search.svg" alt="Search" />

            <input
              @input="onChangeSearchInput"
              class="border border-slate-200 rounded-md py-2 pl-11 pr-4 outline-none focus:border-gray-400"
              placeholder="Поиск..."
              type="text"
            />
          </div>
        </div>
      </div>

      <div class="mt-10">
        <CardList :items="items" />
      </div>
    </div>
  </div>
</template>
