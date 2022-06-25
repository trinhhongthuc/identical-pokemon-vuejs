<template>
  <section class="final-page">
    <h1 class="final-page__title">Chúc mừng bạn đã hoàn thành trò chơi</h1>
    <p class="final-page__description">
      Thời gian hoàn thành:
      <span class="final-page__description-time"
        >{{ Math.ceil((timerFinish - timer) / 1000) }} second</span
      >
    </p>
    <button @click="onRedirectHomePage">Start again</button>
  </section>
</template>

<script>
export default {
  name: "FinalPage",
  data() {
    return {
      timerFinish: new Date().getTime(),
    };
  },
  props: {
    timer: {
      type: Number,
      require: true,
    },
  },
  methods: {
    onRedirectHomePage() {
      this.$emit("onRedirectHomePage", "start-page");
    },
  },
};
</script>
<style scoped>
.final-page {
  height: 100vh;
  max-height: 100vh;
  width: 100%;

  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

.final-page__title {
  font-size: 2.5rem;
  color: var(--color-white);
  margin-bottom: 12px;
}

.final-page__description {
  color: var(--color-white);
  font-size: 2rem;
  margin-bottom: 12px;
}

.final-page__description-time {
  color: var(--color-white);
  font-size: 2.2rem;
}

button {
  padding: 6px 18px;
  cursor: pointer;
}
</style>
