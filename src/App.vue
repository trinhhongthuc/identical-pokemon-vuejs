<template>
  <start-page
    v-if="currentPage === 'start-page'"
    @onStartGame="onStartGamePokemon($event)"
  />
  <main-content-page
    v-if="currentPage === 'main-content-page'"
    :pokemonList="pokemonList"
    @redirectToFinalPage="redirectToFinalPage($event)"
  />
  <final-page
    v-if="currentPage === 'final-page'"
    @onRedirectHomePage="redirectToFinalPage($event)"
    :timer="timer"
  />
</template>

<script>
import StartPage from "./components/StartPages.vue";
import MainContentPage from "./components/MainContentPage.vue";
import FinalPage from "./components/FinalPage.vue";

export default {
  name: "App",
  components: {
    StartPage,
    MainContentPage,
    FinalPage,
  },
  data() {
    return {
      currentPage: "start-page",
      pokemonList: [],
      timer: null,
    };
  },
  methods: {
    onStartGamePokemon(pokemon) {
      const pokemonList = Array.from(
        { length: Number(pokemon.countPokemon) / 2 },
        (v, i) => i + 1
      );

      const resultQuantityPokemon = [...pokemonList]
        .concat(pokemonList)
        .sort(() => Math.random() - 0.5);

      this.pokemonList = resultQuantityPokemon;

      this.timer = new Date().getTime();

      console.log(this.timer);

      this.currentPage = "main-content-page";
    },

    redirectToFinalPage(page) {
      this.currentPage = page;
    },
  },
};
</script>
