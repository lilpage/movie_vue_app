<template>
  <div class="movie-edit">
    <form v-on:submit.prevent="movieEdit(movie)">
      <h1>Edit</h1>
      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>
      <div class="form-group">
        <label>Title: </label> 
        <input type="text" class="form-control" v-model="movie.title">
      </div>
      <div class="form-group">
        <label>Year: </label>
        <input type="text" class="form-control" v-model="movie.year">
      </div>
      <div class="form-group">
        <label>Director: </label>
        <input type="text" class="form-control" v-model="movie.director">
      </div>
      <div class="form-group">
        <label>Plot: </label>
        <input type="text" class="form-control" v-model="movie.plot">
      </div>
      <input type="submit" class="btn btn-primary" value="Submit">
    </form>
  <!-- Delete Action -->
    <button v-on:click="movieDestroy(movie)">Delete</button>
  </div>

</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      movie: {},
      errors: [],
    };
  },
  created: function () {
    axios.get("/api/movies/" + this.$route.params.id).then((response) => {
      console.log(response.data);
      this.movie = response.data;
    });
  },
  methods: {
    movieEdit: function (movie) {
      let params = {
        title: movie.title,
        year: movie.year,
        director: movie.director,
        plot: movie.plot,
      };
      axios.patch("/api/movies/" + this.$route.params.id, params).then(() => {
        this.$router.push("/movies/" + this.movie.id);
      });
    },
    movieDestroy: function (movie) {
      axios.delete("/api/movies/" + movie.id).then(() => {
        console.log("Deleted!");
        this.$router.push("/movies");
      });
    },
  },
};
</script>