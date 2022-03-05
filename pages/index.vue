<template>
  <div v-if="movies.length > 0">
    <section>
      <img
        :src="'https://image.tmdb.org/t/p/original' + movies[0].poster_path"
        alt="Movie Poster"
        class="movie-banner"
      />
      <h1>🎥 {{ movies[0].original_title }}</h1>
      <p class="synopsis">{{ movies[0].overview }}</p>
      <form class="button-container">
        <button class="cta-white">🍿 Add to List</button>
        <button class="cta-transparent">📖 More information</button>
      </form>
      <div class="gradient"></div>
    </section>
    <section>
      <h2>🎉 Latest</h2>
      <div id="movie-grid" class="movie-grid">
        <div class="movie" v-for="(movie, index) in movies" :key="index">
          <img
            :src="`https://image.tmdb.org/t/p/w500${movie.poster_path}`"
            alt="Movie Poster"
            class="movie-poster"
          />
          <NuxtLink
            class="more-info-button"
            :to="{ name: 'movies-movieid', params: { movieid: movie.id } }"
            >More Info</NuxtLink
          >
        </div>
      </div>
    </section>

    <section>
      <h2>🍿 Trending</h2>
      <div id="movie-grid" class="movie-grid">
        <div
          class="movie"
          v-for="(randomMovie, index) in randomMovies"
          :key="index"
        >
          <img
            :src="`https://image.tmdb.org/t/p/w500${randomMovie.poster_path}`"
            alt="Movie Poster"
            class="movie-poster"
          />
          <NuxtLink
            class="more-info-button"
            :to="{
              name: 'movies-movieid',
              params: { movieid: randomMovie.id },
            }"
            >More Info</NuxtLink
          >
        </div>
      </div>
    </section>

    <section>
      <h2>📽 Upcoming</h2>
      <div id="movie-grid" class="movie-grid">
        <div
          class="movie"
          v-for="(upcomingMovie, index) in upcomingMovies"
          :key="index"
        >
          <img
            :src="`https://image.tmdb.org/t/p/w500${upcomingMovie.poster_path}`"
            alt="Movie Poster"
            class="movie-poster"
          />
          <NuxtLink
            class="more-info-button"
            :to="{
              name: 'movies-movieid',
              params: { movieid: upcomingMovie.id },
            }"
            >More Info</NuxtLink
          >
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  transition: {
    name: "layout",
    mode: "out-in",
  },
  data() {
    return {
      movies: [],
      randomMovies: [],
      upcomingMovies: [],
    };
  },
  async fetch() {
    this.movies = await fetch(
      "https://api.themoviedb.org/3/movie/now_playing?api_key=5b75818e63dfdb396cadedf77425b334&language=en-US&page=1"
    )
      .then((res) => res.json())
      .then((data) => data.results);
    console.log(this.movies);

    this.randomMovies = await fetch(
      "https://api.themoviedb.org/3/movie/popular?api_key=5b75818e63dfdb396cadedf77425b334&language=en-US&page=1"
    )
      .then((res) => res.json())
      .then((data) => data.results);

    this.upcomingMovies = await fetch(
      "https://api.themoviedb.org/3/movie/upcoming?api_key=5b75818e63dfdb396cadedf77425b334&language=en-US&page=1"
    )
      .then((res) => res.json())
      .then((data) => data.results);
    console.log(this.upcomingMovies);
  },
};
</script>

<style scoped>
section:first-child {
  height: 100vh;
  padding: 0 2.5em;
  display: flex;
  flex-direction: column;
  justify-content: center;
  object-fit: cover;
  position: relative;
}

section:first-child::after {
  content: "";
  position: absolute;
  bottom: 0;
  left: 0;
  height: 0;
  padding-bottom: calc(33.5% - 92px + 30px);
  width: 100%;
  background-image: linear-gradient(
    transparent,
    rgba(25, 26, 26, 0.4) 10%,
    rgba(25, 26, 26, 0.6) 20%,
    rgba(25, 26, 26, 0.8) 60%,
    var(--dark-grey)
  );
  z-index: -1;
}

section:not(first-child) {
  padding: 3em 2.5em 0;
}

.movie-banner {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center;
  position: absolute;
  left: 0;
  z-index: -1;
  opacity: 0.8;
}

h1,
p {
  padding: 0;
  margin: 0;
  text-shadow: 2px 2px 4px rgb(0 0 0 / 45%);
}

h1 {
  font-size: 3rem;
  max-width: 20em;
}

.synopsis {
  font-size: 1.4vw;
  width: 100%;
  max-width: 30em;
  padding-top: 0.5rem;
  padding-bottom: 1rem;
}

button {
  all: unset;
  padding: 0.7rem 1.7rem;
  font-weight: bold;
  cursor: pointer;
}

.more-info-button {
  background-color: var(--red);
  color: var(--white);
  border-radius: 0.5em;
  padding: 0.7em 2em;
}

.more-info-button:hover {
  opacity: 0.9;
}

.cta-white {
  border-radius: 0.5em;
  color: var(--black);
  background-color: var(--white);
}

.cta-white:hover,
.cta-transparent:hover {
  opacity: 0.8;
}

.movie-grid {
  display: flex;
  gap: 1em;
  overflow-x: auto;
  height: 30em;
}

.movie-grid::-webkit-scrollbar {
  height: 5px;
}

.movie-poster {
  max-width: 15em;
  border-radius: 0.5em;
  margin-bottom: 1.5em;
}

.movie {
  position: relative;
}

.cta-transparent {
  border-radius: 0.5em;
  color: var(--white);
  background-color: var(--transparent);
}

@media (max-width: 50em) {
  section:first-child {
    padding: 10em 1em;
  }

  section:not(first-child) {
    padding: 0 1em;
  }

  h1 {
    margin-top: 4em;
    font-size: 2.5rem;
  }

  h2 {
    font-size: 1.3rem;
  }

  .synopsis {
    font-size: 1.2rem;
  }
}
</style>
