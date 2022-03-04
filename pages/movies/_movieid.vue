<template>
  <div>
    <section>
      <img
        :src="`https://image.tmdb.org/t/p/original${movie.poster_path}`"
        alt="Poster Image"
        class="movie-banner"
      />
    </section>
    <section>
      <figure>
        <img
          :src="`https://image.tmdb.org/t/p/w500${movie.poster_path}`"
          alt="Poster Image"
          class="movie-poster"
        />
      </figure>
      <div>
        <p class="popularity-text">⭐ Rating: {{ movie.vote_average }}</p>
        <h2>{{ movie.original_title }}</h2>
        <p>{{ movie.overview }}</p>
        <p>{{movie.genres}}</p>
      </div>
    </section>
  </div>
</template>
<script>
export default {
  name: "single-movie",
  data() {
    return {
      movie: null,
    };
  },

  async asyncData({ params }) {
    const movie = await fetch(
      `https://api.themoviedb.org/3/movie/${params.movieid}?api_key=5b75818e63dfdb396cadedf77425b334&language=en-US&page=1`
    ).then((res) => res.json());
    console.log(movie)
    return { movie };
  },
};
</script>
<style scoped>
h1,
p {
  padding: 0;
  margin: 0;
}

section:first-child {
  height: 70vh;
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
    rgba(25, 26, 26, 0.8) 80%,
    var(--dark-grey)
  );
  z-index: -1;
}

section:nth-child(2) {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: -10em;
}

.popularity-text {
  padding-bottom: .3em;
}

h2 {
  padding: 0;
  margin: 0;
  max-width: 15em;
  font-size: 2rem;
}

p {
  padding: 0;
  margin: 0;
  max-width: 30em;
  font-size: 1.3rem;
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

.movie-poster {
  width: 15em;
}

@media (max-width: 50em) {
  section:nth-child(2) {
    flex-direction: column;
    padding: 0 1em;
    /* text-align: ; */
  }

  h2 {
    font-size: 1.7rem;
  }

  p {
    font-size: 1.2rem;
  }
}
</style>
