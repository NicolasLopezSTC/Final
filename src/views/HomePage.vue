<script setup>
import { onMounted } from 'vue'
import BaseCard from '@/components/BaseCard.vue'
import useCharacters from '@/composables/useCharacters'

const { characters, fetchCharacters, firstLoad } = useCharacters()

onMounted(async () => {
  if (firstLoad.value) {
    await fetchCharacters()

    firstLoad.value = false
  }

  console.log(characters.value[0].id)
})
</script>

<template>
  <button
    title="Load Characters"
    class="z-90 fixed bottom-8 right-8 flex h-20 w-20 items-center justify-center rounded-full bg-slate-900 text-4xl text-white drop-shadow-lg duration-300 hover:scale-110 hover:bg-green-700 hover:drop-shadow-2xl"
    @click="fetchCharacters"
  >
    🐉
  </button>
  <main class="min-h-screen bg-gradient-to-r from-red-600 to-yellow-300">
    <div class="container mx-auto grid grid-cols-8 gap-4 py-8">
      <BaseCard
        v-for="(character, index) in characters"
        :key="index"
        :character="character"
      />
    </div>
  </main>
</template>
