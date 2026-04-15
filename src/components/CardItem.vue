<script setup>
defineProps({
  imageUrl: String,
  title: String,
  price: Number,
})
</script>

<template>
  <div
    class="relative border bg-white border-slate-100 rounded-3xl p-8 cursor-pointer transition hover:-translate-y-2 hover:shadow-xl"
  >
    <img class="absolute top-8 left-8" src="/like-1.svg" alt="Unlike" />
    <img :src="imageUrl" alt="Sneakers" />

    <p class="mt-2">{{ title }}</p>

    <div class="flex justify-between mt-5">
      <div class="flex flex-col">
        <span class="text-slate-400">Цена:</span>
        <b>{{ price }} руб.</b>
      </div>

      <img src="/plus.svg" alt="Plus" />
    </div>
  </div>
</template>
