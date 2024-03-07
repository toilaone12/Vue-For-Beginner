<template>
  <div class="screen">
    <card-flip
      v-for="(card, index) in cardsContext"
      :choose="{ index, card }"
      :key="index"
      :ref="`card-${index}`"
      :imgUrl="`images/${card}.png`"
      @onFlip="checkChoose($event)"
    />
  </div>
</template>

<script>
import CardScreen from "./CardScreen.vue";

export default {
  props: {
    cardsContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  data() {
    return {
      chooses: [],
    };
  },
  components: {
    CardFlip: CardScreen,
  },
  methods: {
    checkChoose(choose) {
      if (this.chooses.length === 2) return false;
      this.chooses.push(choose);
      if (
        this.chooses.length === 2 &&
        this.chooses[0].card === this.chooses[1].card
      ) {
        console.log("right...");
      } else if (
        this.chooses.length === 2 &&
        this.chooses[0].card !== this.chooses[1].card
      ) {
        //dong 2 the
        this.$refs[`card-${this.chooses[0].index}`][0].onListenFlip();
        this.$refs[`card-${this.chooses[1].index}`][0].onListenFlip();
        //reset chooses ve rong
        this.chooses = [];
        console.log("wrong...");
      } else {
        return false;
      }
    },
  },
};
</script>
