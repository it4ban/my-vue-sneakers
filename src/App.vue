<script setup>
import { onMounted, reactive, ref, watch, provide } from 'vue'
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

const fetchFavorites = async () => {
  try {
    const { data: favorites } = await axios.get('https://cca5a6a137f3ca08.mokky.dev/favorites')

    items.value = items.value.map((item) => {
      const favorite = favorites.find((fav) => fav.parentId === item.id)
      if (!favorite) return item

      return {
        ...item,
        isFavorite: true,
        favoriteId: favorite.id,
      }
    })
  } catch (err) {
    console.error('Error fetching favorites:', err)
  }
}

const addToFavorite = async (item) => {
  try {
    item.isFavorite = !item.isFavorite

    if (!item.isFavorite) {
      const obj = {
        parentId: item.id,
      }

      const { data } = await axios.post('https://cca5a6a137f3ca08.mokky.dev/favorites', obj)

      item.favoriteId = data.id
    } else {
      await axios.delete(`https://cca5a6a137f3ca08.mokky.dev/favorites/${item.favoriteId}`)

      item.favoriteId = null
    }
  } catch (error) {
    console.error('Error adding to favorites:', error)
  }
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

    items.value = data.map((obj) => ({
      ...obj,
      isFavorite: false,
      favoriteId: null,
      isAdded: false,
    }))
  } catch (err) {
    console.error('Error fetching items:', err)
  }
}

onMounted(async () => {
  await fetchItems()
  await fetchFavorites()
})
watch(filters, async () => {
  await fetchItems()
  await fetchFavorites()
})
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
        <CardList :items="items" @addToFavorite="addToFavorite" />
      </div>
    </div>
  </div>
</template>
