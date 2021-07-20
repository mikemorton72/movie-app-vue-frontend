<template>
  <div class="home">
    <h1>Simple Movies App</h1>
    <hr />
    <h2>Add New Movie</h2>
    <p>Title: <input type="text" v-model="newMovie.title"></p>
    <p>Year: <input type="text" v-model="newMovie.year"></p>
    <p>Plot: <input type="text" v-model="newMovie.plot"></p>
    <p>Director: <input type="text" v-model="newMovie.director"></p>
    <p>Note: Adding movies with this tool does not yet allow for adding genres or actors</p>
    <button v-on:click="moviesCreate()">Add Movie</button>
    <hr />
    <div v-for="movie in movies">
      <h3> {{ movie.title }} </h3>
      <p> {{ movie.year }} </p>
      <p><strong>Directed by: </strong>{{ movie.director }}</p>
      <p> <strong>Plot: </strong> {{ movie.plot }} </p>
      <p v-if="hasGenre(movie)">
        <span><strong>Genres: </strong>|</span>
        <span v-for="genre in movie.genre_names"> {{ genre }} |</span>
      </p>
      <p v-if="hasActors(movie)">
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
      newMovie: {},
    };
  },
  created: function () {
    this.moviesIndex();
  },
  methods: {
    hasGenre: function (movie) {
      console.log(movie.genre_names.length);
      if (movie.genre_names.length > 0) {
        return true;
      } else {
        return false;
      }
    },
    hasActors: function (movie) {
      if (movie.actors.length > 0) {
        return true;
      } else {
        return false;
      }
    },
    moviesIndex: function () {
      axios.get("/movies").then((response) => {
        this.movies = response.data;
        // console.log(this.movies);
      });
    },
    moviesCreate: function () {
      axios.post("/movies", this.newMovie).then((response) => {
        console.log(response.data);
        this.movies.push(this.newMovie);
        this.newMovie = {};
      });
    },
  },
};
</script>
