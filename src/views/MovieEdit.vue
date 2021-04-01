<template>
  <div class="movie-edit">
    <form v-on:submit.prevent="submit()">
      <h1>Edit</h1>
      <ul>
        <li class="text-danger" v-for="error in errors" v-bind:key="error">
          {{ error }}
        </li>
      </ul>
      <div class="form-group">
        <label>Title: </label> 
        <input type="text" class="form-control" v-model="title">
      </div>
      <div class="form-group">
        <label>Year: </label>
        <input type="text" class="form-control" v-model="year">
      </div>
      <div class="form-group">
        <label>Director: </label>
        <input type="text" class="form-control" v-model="director">
      </div>
      <div class="form-group">
        <label>Plot: </label>
        <input type="text" class="form-control" v-model="plot">
      </div>
      <input type="submit" class="btn btn-primary" value="Submit">
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {};
  },
  created: function () {},
  methods: {},
};
</script>