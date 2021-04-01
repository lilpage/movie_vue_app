<template>
  <div class="movie-index">
     <div v-for="movie in movies" v-bind:key="movie.id">
      <h2>{{ movie.title }}</h2>
      <h3>Director: {{ movie.director }}, Year: {{ movie.year }}</h3>
      <p> {{ movie.plot }} </p>
      <!-- Somethings broken -->
      <router-link v-bind:to="`/movies/${movie.id}`"  >
        <h3>See More</h3>
      </router-link>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      movies: [],
    };
  },
  created: function () {
    this.moviesIndex();
  },
  methods: {
    moviesIndex: function () {
      axios.get("/api/movies").then((response) => {
        this.movies = response.data;
        console.log(response.data);
      });
    },
  },
};
</script>