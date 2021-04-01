<template>
  <div class="movie-show">
    <div>
     {{ movie }}
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
  ceated: function () {
    axios.get("/api/movies/1").then((response) => {
      console.log(response.data);
      this.movie = response.data;
    });
  },
  methods: {},
};
</script>