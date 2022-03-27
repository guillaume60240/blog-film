<template>
  <div class="container mt-5">
    <h3>Actuellement au cinéma</h3>
    <div class="text-start sort-container">
      Trier par :
      <a
        href="#"
        @click.prevent="sortBy('title')"
        :class="sortSelected == 'title' ? 'selected' : ''"
        >Titre</a
      >
      |
      <a
        href="#"
        @click.prevent="sortBy('release_date')"
        :class="sortSelected == 'release_date' ? 'selected' : ''"
        >Date de sortie</a
      >
      |
      <a
        href="#"
        @click.prevent="sortBy('vote_average')"
        :class="sortSelected == 'vote_average' ? 'selected' : ''"
        >Note</a
      >
    </div>
    <div class="d-flex flex-wrap justify-content-center p-2">
      <div v-for="(film, index) in filmsInCinema" :key="index">
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
// @ is an alias to /src

import FilmCard from '../components/FilmCard';
import Pagination from '../components/partials/Pagination';

const api = process.env.VUE_APP_MOVIE_DB_API_KEY;

export default {
  name: 'Home',
  data() {
    return {
      genres: [],
      filmsInCinema: [],
      sortSelected: '',
      page: 1,
      nbrPages: 1,
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
        // console.log(this.genres);
      } catch (error) {
        console.log(error);
      }
    },
    compareEl(preferences) {
      this.sortSelected = preferences;
      if (preferences != 'vote_average') {
        this.filmsInCinema.sort((a, b) => {
          if (a[preferences] < b[preferences]) {
            return -1;
          }
          if (a[preferences] > b[preferences]) {
            return 1;
          }
          return 0;
        });
      } else {
        this.filmsInCinema.sort((a, b) => {
          return b[preferences] - a[preferences];
        });
      }
    },
    sortBy(preferences) {
      this.compareEl(preferences);
    },

    async getLastMovies() {
      let url = `https://api.themoviedb.org/3/movie/now_playing?api_key=${api}&language=fr-FR`;

      url += `&page=${this.page}`;
      try {
        const response = await axios.get(`${url}`);
        this.filmsInCinema = response.data.results;
        this.nbrPages = response.data.total_pages;

        console.log(
          'getLastMovies : ' +
            this.page +
            ' / ' +
            this.sortSelected +
            ' / ' +
            url
        );
      } catch (error) {
        console.log(error);
      }
    },

    changePage(page) {
      this.page = page;
      console.log('changePage : ' + this.page);
      this.getLastMovies();
    },
  },

  created() {
    console.log('Home created');
    this.getLastMovies();
    this.getMovieGenres();
  },
};
</script>

<style lang="scss" scoped>
.container {
  max-width: 1200px;
  margin: 0 auto;

  .sort-container {
    a {
      color: rgb(12, 11, 11);
      font-weight: bold;
      text-decoration: none;
      padding: 0.5rem;
      margin: 0.5rem;
    }
    .selected {
      color: #42b983;
    }
  }
}
</style>
