<!-- components/Randomizer.vue -->
<script setup>
import { ref, onMounted } from 'vue';

const movie = ref({
  title: 'Loading...',
  genre: '',
  poster: ''
});

// Your TMDB API Key
const apiKey = '15b83cb24b2f0247fdd339f5efae108e';  // Replace with your actual TMDB API key

const fetchMovie = async () => {
  try {
    // Fetch popular movies
    const response = await fetch(`https://api.themoviedb.org/3/movie/popular?api_key=${apiKey}&language=en-US&page=1`);
    const data = await response.json();

    if (data.results && data.results.length > 0) {
      // Pick a random movie from the popular movies list
      const randomMovie = data.results[Math.floor(Math.random() * data.results.length)];

      // Fetch detailed info for the selected movie
      const movieResponse = await fetch(`https://api.themoviedb.org/3/movie/${randomMovie.id}?api_key=${apiKey}&language=en-US`);
      const movieData = await movieResponse.json();

      // Update the movie object with the detailed info
      movie.value = {
        title: movieData.title,
        genre: movieData.genres.map(genre => genre.name).join(', '), // Multiple genres
        poster: `https://image.tmdb.org/t/p/w500${movieData.poster_path}`, // Construct the poster URL
      };
    }

  } catch (error) {
    console.error('Error fetching movie:', error);
  }
};

// Automatically fetch a movie when the component mounts
onMounted(() => {
  fetchMovie();
});
</script>

<template>
  <div class="randomizer">
    <h2>Title: {{ movie.title }}</h2>
    <p>Genre: {{ movie.genre }}</p>
    <img :src="movie.poster" alt="Movie Poster" v-if="movie.poster" />
    <button @click="fetchMovie">Get New Movie</button>
    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Ex tenetur rem perferendis magnam id aliquam quae in
      inventore dolores cupiditate eum minus tempora iusto doloribus enim harum, aperiam quisquam animi.</p>
  </div>
</template>

<style>
.randomizer {
  display: flex;
  flex-direction: column;
  width: 20vw;
}

.randomizer img {
  width: 250px;
  max-height: 300px;
  object-fit: cover;
  padding: 50px;
}
</style>
