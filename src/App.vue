<script setup lang="ts">
import {ref, onMounted, computed, watch } from 'vue'

const todos = ref([])
const name = ref('')

const input_content = ref('')
const inpt_category = ref(null)

const todos_asc = computed(() => todos.value.sort((a, b) => {
  return a.createdAt - b.createdAt
}))

watch(name, (newVal) => {
  localStorage.setItem('name', newVal)
})
</script>

<template>

  <main class="app">
    <section class="gretting">
      <h2 class="title">
        Quoi de neuf,  <input type="text" placeholder="Ton nom ici" v-model="name" />
      </h2>
    </section>
  </main>

</template>