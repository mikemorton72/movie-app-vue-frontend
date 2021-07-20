<template>
  <div class="home">
    <h1>Simple Movies App</h1>
    <hr />
    <div v-for="movie in movies">
      <h3> {{ movie.title }} </h3>
      <p> {{ movie.year }} </p>
      <p><strong>Directed by: </strong>{{ movie.director }}</p>
      <p> <strong>Plot: </strong> {{ movie.plot }} </p>
      <p>
        <span><strong>Genres: </strong>|</span>
        <span v-for="genre in movie.genre_names"> {{ genre }} |</span>
        

      </p>
      <p>
      <span><strong>Actors:</strong></span>
      <span v-for="actor in movie.actors"> {{ actor.first_name }} {{ actor.last_name }}, </span>
      </p>
      <hr />
    </div>
  </div>
</template>

<style></style>

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
      axios.get("/movies").then((response) => {
        this.movies = response.data;
        console.log(this.movies);
      });
    },
  },
};
</script>
