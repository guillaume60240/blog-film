<template>
  <div class="card">
    <Modale
      :film="film"
      :genres="this.genres"
      :modalWatched="this.modalWatched"
      :toggleModale="this.toggleModale"
    />

    <div class="card-body text-start">
      <span @click="toggleModale"><div class="circle"></div></span>
      <img
        :src="'https://image.tmdb.org/t/p/w500' + film.poster_path"
        :alt="'Affiche du film' + film.title"
      />
      <Note :note="film.vote_average" />
    </div>
    <div class="card-footer text-start ps-0 mt-4">
      <p class="mb-1">
        <strong>{{ film.title }}</strong>
      </p>
      <small>
        {{
          new Date(film.release_date).toLocaleDateString('fr', this.dateOptions)
        }}
      </small>
      <!--<div class="d-flex justify-content-around align-items-center"> -->
      <!-- <strong>Genre :</strong>
        {{
          film.genre_ids
            .map(
              (genreId) =>
                this.genres.find((genre) => genre.id === genreId).name
            )
            .join(', ')
        }} -->
      <!-- <p class="text-start">genres :</p>
        <div>
          <a
            href=""
            v-for="(genre, index) in this.assignGenres(this.film, this.genres)"
            :key="index"
          >
            <small
              ><i>{{ genre.name }} </i> </small
            ><br />
          </a>
        </div>
      </div> -->
    </div>
  </div>
</template>

<script>
// const api = process.env.VUE_APP_MOVIE_DB_API_KEY;
import Note from './partials/Note';
import Modale from './partials/FilmModal';

export default {
  name: 'FilmCard',
  data() {
    return {
      //pour gérer l'affichage de la date
      dateOptions: {
        year: 'numeric',
        month: 'long',
        day: 'numeric',
      },
      //pour gérer l'affichage des genres
      filmGenres: [],
      //pour gérer l'affichage de la modale
      modalWatched: false,
    };
  },
  props: {
    film: {
      type: Object,
      required: true,
    },
    genres: {
      type: Array,
      required: true,
    },
  },
  components: {
    Note,
    Modale,
  },

  methods: {
    toggleModale() {
      this.modalWatched = !this.modalWatched;
    },
  },
};
</script>

<style lang="scss" scoped>
.card {
  position: relative;
  margin-bottom: 20px;
  width: 250px;
  border: none;
  background: none;

  .card-header {
    border: none;
    background: none;
    min-height: 92px;
  }
  .card-body {
    padding: 0;
    position: relative;

    span {
      position: absolute;
      top: 10px;
      left: 10px;
      opacity: 0.6;
      color: #000;

      .circle {
        position: relative;
        top: 0;
        left: 0;
        display: inline-flex;
        align-items: center;
        min-width: 1.5em;
        min-height: 1.5em;
        line-height: inherit;
        background-image: url(../assets/glyphicons-basic-947-circle-more-white-4c440dfc1b0e626c70f4853dbbce9c4d1f2c5d8f3e05a7d3df47881cbd816adf.svg);
        background-position: center center;
        background-repeat: no-repeat;
        color: inherit;
        box-sizing: border-box;
        cursor: pointer;
      }
    }

    img {
      width: auto;
      max-height: 250px;
      border-radius: 10px;
    }
  }
  .card-footer {
    background: none;
    border: none;
    line-height: 1.2em;
  }
}
</style>
