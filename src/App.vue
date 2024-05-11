<script setup>
import {ref, onMounted, computed, watch } from 'vue'

const todos = ref([])
const name = ref('')

const input_content = ref('')
const input_category = ref(null)

const todos_asc = computed(() => todos.value.sort((a, b) => {
  return a.createdAt - b.createdAt
}))

const addTodo = () => {
  if (input_content.value.trim() === '' || input_category.value === null) {
    return
  } 

  todos.value.push({
    content: input_content.value,
    category: input_category.value,
    done: false,
    createdAt: new Date.getTime()
  })
}

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

        <form @submit.prevent="addTodo">
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
              <div>Personnel</div>
            </label>

          </div>

          <input type="submit" value="Add todo" />

        </form>
      </section>

  </main>

</template>