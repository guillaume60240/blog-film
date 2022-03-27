<template>
  <div class="container mt-5">
    <h3>{{ this.category.name }}</h3>
    <div class="d-flex flex-wrap justify-content-center p-2">
      <div v-for="(film, index) in films" :key="index">
        <filmCard :film="film" :genres="genres" />
      </div>
    </div>
    <Pagination
      :page="this.page"
      :nbrPages="this.nbrPages"
      v-on:change-page="changePage($event)"
    />
  </div>
</template>

<script>
import axios from 'axios';

const api = process.env.VUE_APP_MOVIE_DB_API_KEY;

import FilmCard from '../components/FilmCard';
import Pagination from '../components/partials/Pagination';

export default {
  name: 'FilmByCategory',
  data() {
    return {
      genres: [],
      films: [],
      sortSelected: '',
      page: 1,
      nbrPages: 1,
      category: '',
    };
  },
  components: {
    FilmCard,
    Pagination,
  },
  methods: {
    async getMovieGenres() {
      try {
        const response = await axios.get(
          `https://api.themoviedb.org/3/genre/movie/list?api_key=${api}&language=fr-FR`
        );
        this.genres = response.data.genres;
        this.category = this.genres.find(
          (genre) => genre.id == this.$route.params.id
        );

        console.log(this.genres);
      } catch (error) {
        console.log(error);
      }
    },
    async getMovieByCategories(categoryId) {
      let url = `https://api.themoviedb.org/3/discover/movie?api_key=${api}&language=fr-FR&sort_by=popularity.desc&include_adult=true&include_video=false&page=${this.page}&with_genres=${categoryId}`;

      axios
        .get(url)
        .then((response) => {
          this.films = response.data.results;
          this.nbrPages = response.data.total_pages;
        })
        .catch((error) => {
          console.log(error);
        });
    },
    changePage(page) {
      this.page = page;
      console.log('changePage : ' + this.page);
      this.getMovieByCategories(this.$route.params.id);
    },
  },
  beforeMount() {
    console.log('beforeMount');
    this.getMovieGenres();
  },
  mounted() {
    console.log('mounted');
  },
  beforeUpdate() {
    console.log('beforeUpdate');
  },
  updated() {
    console.log('updated');
    // this.getMovieByCategories(this.$route.params.id);
  },
  beforeCreate() {
    console.log('beforeCreate');
  },
  created() {
    this.categoryId = this.$route.params.id;
    this.getMovieByCategories(this.$route.params.id);
  },
};
</script>

<style lang="scss" scoped>
.conatiner {
  max-width: 1200px;
  margin: 0 auto;
}
</style>
