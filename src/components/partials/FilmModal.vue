<template>
  <div class="modale-container" v-if="modalWatched">
    <div class="content">
      <div>
        <p class="text-end close-modale" @click="toggleModale">X</p>
      </div>
      <div class="d-flex flex-column justify-content-between text-start">
        <p class="m-0">Genres :</p>
        <span v-for="(genre, index) in assignGenres(genres, film)" :key="index">
          <router-link
            :to="{ name: 'Categorie', params: { id: genre.id } }"
            class="nav-link"
            ><i>{{ genre.name }}</i></router-link
          >
        </span>
      </div>
      <div class="mt-3 text-start">
        <p class="">
          <router-link :to="{ name: 'Film', params: { id: film.id } }"
            >Voir plus..</router-link
          >
        </p>
      </div>
    </div>
    <div></div>
  </div>
</template>

<script>
export default {
  name: 'Modale',
  data() {
    return {
      modal: false,
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
    modalWatched: {
      type: Boolean,
      default: false,
    },
    toggleModale: {
      type: Function,
    },
  },
  methods: {
    assignGenres(genres, film) {
      let filmGenres = genres.filter((genre) =>
        film.genre_ids.includes(genre.id)
      );
      return filmGenres;
    },
  },
  beforeMount() {
    console.log('beforeMount');
  },
  mounted() {
    console.log('mounted');
    // this.assignGenres(this.film, this.genres);
  },
  beforeUpdate() {
    console.log('beforeUpdate');
  },
  updated() {
    console.log('updated');
    // this.assignGenres(this.film, this.genres);
  },
  beforeCreate() {
    console.log('beforeCreate');
  },
  created() {
    console.log('created');
  },
  beforeDestroy() {
    console.log('beforeDestroy');
  },
  destroyed() {
    console.log('destroyed');
  },
};
</script>

<style lang="scss">
.modale-container {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  //   align-items: center;
  width: 80%;
  height: 83%;
  background-color: rgba(0, 0, 0, 0.735);
  position: absolute;
  top: 0;
  left: 0;
  z-index: 100;
  padding: 1em;
  color: aliceblue;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.735);
  .content {
    position: relative;
    width: 100%;
    height: 100%;

    .close-modale {
      position: absolute;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      top: 0;
      right: 0;
      font-size: 1em;
      width: 2em;
      height: 2em;
      //   border: solid 1px aliceblue;
      background: rgba(240, 248, 255, 0.331);
      border-radius: 50%;
      color: aliceblue;
      cursor: pointer;
    }
  }

  a {
    color: aliceblue;
    text-decoration: none;
    cursor: pointer;

    &:hover {
      color: aliceblue;
      text-decoration: underline;
    }
  }
}
</style>
