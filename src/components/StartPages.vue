<template>
  <section class="start-page">
    <h1 class="start-page__title">Pokemon memories</h1>
    <h3 class="start-page__sub-title">Select mode to start</h3>
    <div class="start-page__action">
      <button @click="onStartGame(16)">
        <span> 4x4 </span>
        <span> easy </span>
      </button>
      <button @click="onStartGame(36)">
        <span> 6x6 </span>
        <span> normal </span>
      </button>
      <button @click="onStartGame(64)">
        <span> 8x8 </span>
        <span> hard </span>
      </button>
      <button @click="onStartGame(100)">
        <span> 10x10 </span>
        <span> supper hard </span>
      </button>
    </div>
  </section>
</template>

<script>
export default {
  name: "StartPage",
  methods: {
    onStartGame(countPokemon) {
      this.$emit("onStartGame", { countPokemon });
    },
  },
};
</script>

<style lang="css" scoped>
.start-page {
  display: flex;
  align-items: center;
  justify-content: center;

  flex-direction: column;
  width: 100%;
  max-height: 100vh;
  height: 100vh;
}

.start-page__title {
  font-size: 2.3rem;
  margin-bottom: 12px;
  color: var(--color-white);
}

.start-page__sub-title {
  font-size: 1.8rem;
  margin-bottom: 12px;
  color: var(--color-white);
}

.start-page__action {
  display: flex;
}

.start-page__action button {
  width: 80px;
  height: 80px;
  outline: none;
  border-radius: 8px;
  border: 1px solid #fff;
  background: var(--color-dark);

  display: flex;
  align-items: center;
  justify-content: center;

  flex-direction: column;
  color: #fff;
  margin-right: 12px;
}

.start-page__action button:hover {
  background: var(--color-light);
  color: var(--color-dark);
  cursor: pointer;
  transition: all 0.6s ease;
}
</style>
