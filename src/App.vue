<template>
  <div id="app">
    <!-- Navbar content -->
    <div id="nav">
      <nav class="navbar navbar-expand-lg navbar-dark bg-dark p-3">
        <div class="container-fluid">
          <router-link class="navbar-brand text-white" to="/"
            >Mon CarnetCiné</router-link
          >
          <button
            class="navbar-toggler"
            type="button"
            data-bs-toggle="collapse"
            data-bs-target="#navbarNavAltMarkup"
            aria-controls="navbarNavAltMarkup"
            aria-expanded="false"
            aria-label="Toggle navigation"
          >
            <span class="navbar-toggler-icon"></span>
          </button>
        </div>

        <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
          <div class="navbar-nav">
            <router-link to="/" class="nav-link">Accueil</router-link>
            <router-link to="/about" class="nav-link">Mes films</router-link>
          </div>
        </div>
      </nav>
    </div>
    <div class="head p-3">
      <div class="header-text-container">
        <p class="pt-5 text-start header-title">Bienvenue,</p>
        <p class="text-start header-subtitle">
          Des millions de films à découvrir!!
        </p>
      </div>
      <form class="d-flex nav-form mt-5">
        <input
          class="form-control me-2"
          type="search"
          placeholder="Rechercher un film, une série..."
          aria-label="Search"
        />
        <button class="btn" type="submit">Search</button>
      </form>
    </div>
    <router-view />
  </div>
</template>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  // padding: 30px;
  #navbarNavAltMarkup {
    // flex-basis: 1;
    min-width: 200px;
    // .navbar-nav {
    //   margin-left: auto;
    //   margin-right: auto;
    //   width: auto;
    // }
  }

  a {
    font-weight: bold;
    // color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
.head {
  font-size: 2em;
  font-weight: bold;
  color: #e2ede8;
  max-width: 1500px;
  height: 300px;
  background-image: linear-gradient(
      rgba(36, 33, 33, 0.6),
      rgba(41, 42, 50, 0.6)
    ),
    url('./assets/header.jpg');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;

  margin: 0 auto;
  .header-text-container {
    line-height: 1em;
    margin-bottom: 4rem;
    .header-title {
      font-size: 2em;
      font-weight: bold;
    }
  }

  .nav-form {
    min-width: 400px;
    max-width: 600px;

    button {
      background-color: #42b983;
      color: #e2ede8;
      border: none;
      border-radius: 5px;
      padding: 5px 10px;
      font-size: 1rem;
      cursor: pointer;
    }
  }
}
</style>
