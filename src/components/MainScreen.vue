<template>
  <div class="screen">
    <h1>POKEMON MEMORIES</h1>
    <h3>Select mode to start game</h3>
    <div class="modes">
      <button
        v-for="modeGame in modeGames"
        :key="modeGame.mode"
        @click="onStart(modeGame.id)"
      >
        <span>{{ modeGame.mode }}</span>
        <span>{{ modeGame.challenge }}</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      modeGames: [
        {
          id: 16,
          mode: "4x4",
          challenge: "Easy",
        },
        {
          id: 36,
          mode: "6x6",
          challenge: "Normal",
        },
        {
          id: 64,
          mode: "8x8",
          challenge: "Hard",
        },
        {
          id: 100,
          mode: "10x10",
          challenge: "Super Hard",
        },
      ],
    };
  },
  methods: {
    onStart(totalCard) {
      this.$emit("onStart", { totalCard });
    },
  },
};
</script>
