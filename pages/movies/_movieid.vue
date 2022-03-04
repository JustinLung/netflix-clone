<template></template>
<script>
export default {
  name: "single-movie",
  data() {
    return {
      movie: null,
    };
  },

  async fetch() {
    this.movies = await fetch(
      `https://api.themoviedb.org/3/movie/${this.$route.params.movieid}?api_key=5b75818e63dfdb396cadedf77425b334&language=en-US&page=1`
    )
      .then((res) => res.json())
      .then((data) => {
        return data.results;
      });
      console.log(this.movies)
  },
};
</script>
<style scoped></style>
