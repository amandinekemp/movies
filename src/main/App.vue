<template>
  <p>Compteur : {{ count }}</p>
  <button @click="increment">Incrémenter</button>
  <button @click="decrement">Décrémenter</button>
  <hr>
  <button @click="sortMovies">Réorganiser</button>
  <form @submit.prevent="addMovie">
    <input type="text" placeholder="Nouveau film" v-model="movieName" />
    <button>Ajouter</button>
  </form>
  <ul>
    <li v-for="movie in movies" :key="movie">
      {{ movie }} <button @click="deleteMovie(movie)">Supprimer</button>
    </li>
  </ul>
</template>

<script setup>
import { ref } from 'vue'

const count = ref(0)
const movieName = ref('')
const movies = ref([
  'Matrix',
  'Lilo et Stich',
  'Titanic'
])

const increment = () => {
  count.value++
}

const decrement = () => {
  count.value--
}

const deleteMovie = (movie) => {
  movies.value = movies.value.filter(m => m !== movie)
}

const sortMovies = () => {
  movies.value.sort((a, b) => (a > b ? 1 : -1))
}

const addMovie = () => {
  if (movieName.value.trim()) {
    movies.value.push(movieName.value.trim())
    movieName.value = ''
  }
}
</script>
