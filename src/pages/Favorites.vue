<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'

import Cartlist from '../components/CartList.vue'

const favorites = ref([])

onMounted(async () => {
  try {
    const { data } = await axios.get(
      'https://15d3fa91fbccc9db.mokky.dev/favorites?_relations=items'
    )

    favorites.value = data.map((obj) => obj.item)
  } catch (err) {
    console.log(err)
  }
})
</script>

<template>
  <h1 class="text-3xl font-bold mb-8">Мои закладки</h1>

  <div class="mt-10">
    <Cartlist :items="favorites" is-favorites />
  </div>
</template>
