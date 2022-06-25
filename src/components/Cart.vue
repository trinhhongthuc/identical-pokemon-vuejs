<template>
  <div class="card" :class="{ disable: disable }">
    <div
      class="card__inner"
      :class="{ 'is-flipped': isActive }"
      @click="onRotatePokemon"
    >
      <div class="card__face card__face--front">
        <div class="card__content"></div>
      </div>
      <div class="card__face card__face--back">
        <div
          class="card__content"
          :style="{
            backgroundImage: `url('${require('@/assets/images/' +
              srcPokemon +
              '.png')}')`,
          }"
        ></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "CartComponent",
  props: {
    srcPokemon: {
      type: Number,
      require: true,
    },
    index: {
      type: Number,
      require: true,
    },
  },
  data() {
    return {
      isActive: false,
      disable: false,
    };
  },
  methods: {
    onRotatePokemon() {
      this.$emit("clickToCartPokemon", {
        index: this.srcPokemon,
        valuePokemon: this.index,
      });
      this.isActive = !this.isActive;
    },
    onDisableActive() {
      this.isActive = false;
    },
  },
};
</script>

<style lang="css" scoped>
.card {
  display: inline-block;
  margin-right: 1rem;
  margin-bottom: 1rem;
}

.card.disable {
  pointer-events: none;
}
.card__inner {
  width: 90px;
  height: 120px;
  transition: transform 1s;
  transform-style: preserve-3d;
  cursor: pointer;
  position: relative;
}
.card.disabled .card__inner {
  cursor: default;
}
.card__inner.is-flipped {
  transform: rotateY(-180deg);
}
.card__face {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  overflow: hidden;
  border-radius: 1rem;
  padding: 1rem;
  box-shadow: 0 3px 18px 3px rgba(0, 0, 0, 0.2);
}
.card__face--front .card__content {
  background: url("@/assets/images/icon_back.png") no-repeat center center;
  background-size: 30px 30px;
  height: 100%;
  width: 100%;
}
.card__face--back {
  background-color: var(--color-light);
  transform: rotateY(180deg);
}
.card__face--back .card__content {
  background-position: center center;
  background-repeat: no-repeat;
  background-size: contain;
  height: 100%;
  width: 100%;
}
</style>
