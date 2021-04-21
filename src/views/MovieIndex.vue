<template>
  <div class="container movies-index">
    Search by name:
    <input v-model="titleFilter" list="titles" />
    <datalist id="titles">
      <option v-for="movie in movies" v-bind:key="movie.id">{{ movie.title }}</option>
    </datalist>
    <div><button v-on:click="orderBy(movie.title)">Sort Alphabetically</button></div>
    <div
      v-for="movie in orderBy(filterBy(movies, titleFilter, 'title'), 'title')"
      v-bind:key="movie.id"
      class="card mb-3"
      style="max-width: 540px"
    >
      <div class="row no-gutters">
        <div class="col-md-8">
          <div class="card-body">
            <h3 class="card-title">{{ movie.title }}</h3>
            <h5 class="card=text">{{ movie.director }} ({{ movie.year }})</h5>
            <p class="card-text">
              {{ movie.plot }}
            </p>
          </div>
        </div>
      </div>
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