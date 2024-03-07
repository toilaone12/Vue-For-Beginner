<template>
  <div class="card">
    <div
      class="card-inner"
      @click="onToggleFlipCard"
      :class="{ 'card-flipped': isFlip }"
    >
      <div class="card-face card-front">
        <div class="card-content"></div>
      </div>
      <div class="card-face card-back">
        <div
          class="card-content"
          :style="{ backgroundImage: `url(${require('@/assets/' + imgUrl)})` }"
        ></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    imgUrl: {
      type: String,
      required: true,
    },
    choose: {
      type: [String, Number, Array, Object], // 1 trong 4 loai
    },
  },
  data() {
    return {
      isFlip: false,
    };
  },
  methods: {
    onToggleFlipCard() {
      this.isFlip = !this.isFlip;
      if (this.isFlip) this.$emit("onFlip", this.choose);
    },
    onListenFlip() {
      this.isFlip = false;
    },
  },
};
</script>

<style lang="css" scoped>
.card {
  display: inline-block;
  width: 90px;
  height: 120px;
  margin: 1rem 1rem 0 0;
}
.card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  transition: transform 1s;
  transform-style: preserve-3d;
  cursor: pointer;
}
.card-inner.card-flipped {
  transform: rotateY(-180deg);
}
.card-face {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  overflow: hidden;
  border-radius: 0.5rem;
  padding: 1rem;
  box-shadow: 0 3px 10px 3px rgba(0, 0, 0, 0.2);
}
.card-back {
  background-color: var(--light);
  transform: rotateY(-180deg);
}
.card-front .card-content {
  background: url("../assets/images/icon_back.png") no-repeat center center;
  background-size: 50px 50px;
  width: 100%;
  height: 100%;
}
.card-back .card-content {
  background-size: contain;
  background-position: center;
  background-repeat: no-repeat;
  height: 100%;
  width: 100%;
}
</style>
