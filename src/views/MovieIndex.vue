<template>
  <div class="movie-index">
     <div v-for="movie in movies" v-bind:key="movie.id">
        <h2>{{ movie.title }}</h2>
        <h3>Director: {{ movie.director }}, Year: {{ movie.year }}</h3>
        <p> {{ movie.plot }} </p>
        <router-link v-bind:to="`/movies/${movie.id}`"  >
          <h3>See More</h3>
        </router-link>
        <!-- Search -->
      </div>
        Search by title: <input v-model="titleFilter">
        <div v-for="movie in filterBy(movies, titleFilter, 'title')" v-bind:key="movie.id">
        </div>
        Search by name: <input v-model="titleFilter" list="titles">
        <datalist id="titles">
          <option v-for="movie in movies" v-bind:key="movie.id">{{ movie.title }}</option>
        </datalist>
      <!-- Sort -->
      <div>
        <button>Sort Alphabetically</button>
        <div v-for="movie in orderBy(movies, 'title')">
         <div v-for="movie in orderBy(filterBy(movies, titleFilter, 'title'), 'title')"> 
      </div>
  </div>
</template>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function () {
    return {
      movies: [],
      titleFilter: "",
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