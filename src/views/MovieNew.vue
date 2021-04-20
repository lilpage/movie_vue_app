<template>
  <div class="movie-new">
      <h3>Add New Movie</h3>
      Title: <input type="text" v-model="movieTitle"> <br>
      Year: <input type="text" v-model="movieYear"> <br>
      Director: <input type="text" v-model="movieDirector"> <br>
      Plot: <input type="text" v-model="moviePlot"> 
      <small v-if="moviePlot.length >= 500">Limit 500 characters.</small>
       <br> <br>
    <button v-on:click="moviesCreate()">Add Movie</button>
    </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      movieTitle: "",
      movieYear: "",
      movieDirector: "",
      moviePlot: "",
    };
  },
  created: function () {},
  methods: {
    moviesCreate: function () {
      let params = {
        title: this.movieTitle,
        year: this.movieYear,
        director: this.movieDirector,
        plot: this.moviePlot,
      };
      axios.post("/api/movies/", params).then(
        (response) => {
          console.log(response);
          this.movies.push(response.data);
        },
        (error) => {
          console.log(error);
        }
      );
    },
  },
};
</script>