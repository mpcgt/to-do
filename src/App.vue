<script setup lang="ts">
import {ref, onMounted, computed, watch } from 'vue'

const todos = ref([])
const name = ref('')

const input_content = ref('')
const input_category = ref(null)

const todos_asc = computed(() => todos.value.sort((a, b) => {
  return a.createdAt - b.createdAt
}))

const addTodo = () => {}

watch(name, (newVal) => {
  localStorage.setItem('name', newVal)
})

onMounted(() => {
  name.value = localStorage.getItem('name') || ''
})
</script>

<template>

  <main class="app">
    <section class="gretting">
      <h2 class="title">
        Quoi de neuf,  <input type="text" placeholder="Ton nom ici" v-model="name" />
      </h2>
    </section>

      <section class="create-todo">
        <h3>
          Créer un todo
        </h3>

        <form @submit.prevent="addTodo">*
          <h4>
            Quelle est votre liste de choses à faire ?
          </h4>
          <input 
            type="text" 
            placeholder="Ecrivez ici" 
            v-model="input_content" />

          <h4>Choisissez une catégorie</h4>

          <div class="options">

            <label>
              <input 
                type="radio" 
                name="category"
                value="business"
                v-model="input_category" />
              <span class="bubble business"></span>
              <div>Professionnel</div>
            </label>

            <label>
              <input 
                type="radio" 
                name="category"
                value="personal"
                v-model="input_category" />
              <span class="bubble personal"></span>
              <div>Personnem</div>
            </label>
          </div>
        </form>
      </section>

  </main>

</template>