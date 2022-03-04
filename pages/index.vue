<template>
  <div>
    <section>
      <img
        :src="'https://image.tmdb.org/t/p/original' + movies[0].poster_path"
        alt="Movie Poster"
        class="movie-banner"
      />
      <h1>{{ movies[0].original_title }}</h1>
      <p>{{ movies[0].overview }}</p>
      <div class="button-container">
        <button class="cta-white">Add to List</button>
        <button class="cta-transparent">More information</button>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      movies: [],
    };
  },
  async fetch() {
    this.movies = await fetch(
      "https://api.themoviedb.org/3/movie/now_playing?api_key=5b75818e63dfdb396cadedf77425b334&language=en-US&page=1"
    )
      .then((res) => res.json())
      .then((data) => {
        return data.results;
      });
    console.log(this.movies);
  },
};
</script>

<style scoped>
section {
  height: 40em;
  padding: 0 2.5em;
  display: flex;
  flex-direction: column;
  justify-content: center;
  object-fit: cover;
  position: relative;
}

.movie-banner {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center;
  position: absolute;
  left: 0;
  z-index: -1;
  opacity: .8;
}

h1,
p {
  padding: 0;
  margin: 0;
}

h1 {
  font-size: 3rem;
}

p {
  font-size: 1.5rem;
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

.cta-white {
  border-radius: 0.5em;
  color: var(--black);
  background-color: var(--white);
}

.cta-white:hover,
.cta-transparent:hover {
  opacity: 0.8;
}

.cta-transparent {
  border-radius: 0.5em;
  color: var(--white);
  background-color: var(--transparent);
}

@media (max-width: 50em) {
  section {
    padding: 10em 1em;
  }

  h1 {
    font-size: 2.5rem;
  }

  p {
    font-size: 1.2rem;
  }
}
</style>
