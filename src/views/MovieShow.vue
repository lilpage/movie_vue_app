<template>
  <div class="movie-show">
    <div>
      <h2>{{ movie.title }}</h2>
      <h3>Director: {{ movie.director }}, Year: {{ movie.year }}</h3>
      <p> {{ movie.plot }} </p>
     <router-link v-bind:to="`/movies/${movie.id}/edit`">
     <p>Edit</p>
     </router-link>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      movie: {},
    };
  },
  created: function () {
    axios.get("/api/movies/" + this.$route.params.id).then((response) => {
      console.log(response.data);
      this.movie = response.data;
    });
  },
  methods: {},
};
</script>