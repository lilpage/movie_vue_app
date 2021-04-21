<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div class="jumbotron">
      <h1 class="display-4">Movies!</h1>
      <p class="lead">Do you like movies?</p>
      <hr class="my-4">
    <!-- Html Extra Checkbox -->
    <input type="checkbox" name="likeMovies"> <label for="likeMovies"> Yes, I like movies</label>
    <!-- Index -->
    </div>
      <div class="row">
        <div class="col-sm-6" v-for="movie in movies" v-bind:key="movie.id">
          <div class="card">
            <div class="card-body">
              <h2>{{ movie.title }}</h2>
              <h3>Director: {{ movie.director }}, Year: {{ movie.year }}</h3>
              <p> {{ movie.plot }} </p>
            </div>
          </div>
        </div>
      </div>
    <!-- <div v-for="movie in movies" v-bind:key="movie.id"> -->

    <!-- Show -->
      <!-- <button v-on:click="movieShow(movie)">More Info</button>
      <dialog id="movie-info">
        <form method="dialog">
          Title: <input type="text" v-model="currentMovie.title"> <br>
          Year: <input type="text" v-model="currentMovie.year"> <br>
          Director: <input type="text" v-model="currentMovie.director"> <br>
          Plot: <input type="text" v-model="currentMovie.plot"> <br> <br>
          <button>Close</button>
          <button v-on:click="movieUpdate(currentMovie)">Update</button>
          <button v-on:click="movieDelete()">Delete</button>
        </form>
      </dialog>
    </div>
    <br> -->
    <!-- Create -->
    <!-- <div id="create">
      <h3>Add New Movie</h3>
      Title: <input type="text" v-model="movieTitle"> <br>
      Year: <input type="text" v-model="movieYear"> <br>
      Director: <input type="text" v-model="movieDirector"> <br>
      Plot: <input type="text" v-model="moviePlot"> <br> <br>
    <button v-on:click="moviesCreate()">Add Movie</button>
    </div> -->
  </div>
</template>
<style>
div {
  color: white;
  background-color: rgb(245, 166, 180);
}
#create {
  background-color: palevioletred;
  width: 250px;
  margin: 0 auto;
  padding: 25px;
}
.jumbotron {
  background-color: palevioletred !important;
}
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Lil's Fav Movies",
      movies: [],
      movieTitle: "",
      movieYear: "",
      movieDirector: "",
      moviePlot: "",
      currentMovie: {},
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
    movieShow: function (movie) {
      this.currentMovie = movie;
      document.querySelector("#movie-info").showModal();
    },
    movieUpdate: function (movie) {
      let params = {
        title: this.movvieTitle,
        year: this.movieYear,
        director: this.movieDirector,
        plot: this.moviePlot,
      };
      axios.patch("/api/movies/" + movie.id, params).then((response) => {
        console.log("Movie updated." + response);
      });
    },
    movieDelete: function (movie) {
      axios.delete("/api/movies/" + movie.id);
      console.log("Successfully deleted.");
    },
  },
};
</script>