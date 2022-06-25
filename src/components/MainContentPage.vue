<template>
  <div
    class="main-content"
    :style="{
      width: `${
        Math.sqrt(pokemonList.length) * 90 + Math.sqrt(pokemonList.length) * 16
      }px`,
    }"
  >
    <h1 class="main-content__title">Choose two identical pokemon</h1>
    <cart
      v-for="(cart, index) in pokemonList"
      :key="index"
      :srcPokemon="cart"
      :index="index"
      ref="cart"
      @clickToCartPokemon="checkPokemonClick"
    />
  </div>
</template>

<script>
import Cart from "./Cart.vue";

export default {
  name: "MainContentPage",
  components: {
    Cart,
  },
  data() {
    return {
      listMatchPokemon: [],
      pointStopGame: [],
    };
  },
  props: {
    pokemonList: {
      type: Array,
      default: () => [],
    },
  },

  methods: {
    checkPokemonClick(result) {
      if (this.listMatchPokemon.length === 2) return false;

      this.listMatchPokemon.push(result);

      if (
        this.listMatchPokemon.length === 2 &&
        this.listMatchPokemon[0].index === this.listMatchPokemon[1].index
      ) {
        this.$refs.cart[this.listMatchPokemon[0].valuePokemon].disable = true;
        this.$refs.cart[this.listMatchPokemon[1].valuePokemon].disable = true;
        this.pointStopGame.push(...this.listMatchPokemon);
        this.listMatchPokemon = [];

        if (this.pointStopGame.length === this.pokemonList.length) {
          setTimeout(() => {
            this.$emit("redirectToFinalPage", "final-page");
            return true;
          }, 1000);
        }
      } else if (
        this.listMatchPokemon.length === 2 &&
        this.listMatchPokemon[0].index !== this.listMatchPokemon[1].index
      ) {
        setTimeout(() => {
          this.$refs.cart[
            this.listMatchPokemon[0].valuePokemon
          ].isActive = false;
          this.$refs.cart[
            this.listMatchPokemon[1].valuePokemon
          ].isActive = false;
          this.listMatchPokemon = [];
        }, 800);
      } else return false;
    },
  },
};
</script>

<style scoped>
.main-content {
  margin: 0 auto;
  height: 100vh;
  max-height: 100vh;
  width: 1200px;
}

.main-content__title {
  font-size: 2.2rem;
  color: var(--color-white);
  text-align: center;
  padding-bottom: 12px;
  padding-top: 12px;
}
</style>
