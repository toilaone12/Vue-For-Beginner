<template>
  <main-screen
    @onStart="handleStart($event)"
    v-if="statusMatch === 'default'"
  />
  <interact-screen
    v-if="statusMatch === 'inMatch'"
    :cardsContext="settings.cardsContext"
  />
</template>

<script>
import MainScreen from "./components/MainScreen.vue";
import InteractScreen from "./components/InteractScreen.vue";
import { shuffled } from "./utils/array.js";

export default {
  name: "App",
  data() {
    return {
      settings: {
        totalCards: 0,
        cardsContext: [],
        startedAt: null,
      },
      statusMatch: "default",
    };
  },
  components: {
    MainScreen,
    InteractScreen,
  },
  methods: {
    handleStart(e) {
      // eslint-disable-next-line no-console
      this.settings.totalCards = e.totalCard;
      //tao ra 1 mang moi de chia 2 the giong nhau
      const firstCards = Array.from(
        { length: this.settings.totalCards / 2 },
        (_, i) => i + 1 // doi so 1 bo qua, doi so 2 bat dau tu 1 tang dan + 1 den length: tong / 2
      );
      //tao ra mang thu 2 giong mang 1
      const secondCards = [...firstCards];
      //noi 2 mang lai voi nhau
      const compoundCards = [...firstCards, ...secondCards];
      //dung ham shuffled dc tao ben array.js de doi thu tu cac so
      this.settings.cardsContext = shuffled(
        shuffled(shuffled(shuffled(shuffled(compoundCards))))
      );
      this.settings.startedAt = new Date().getTime();
      //data ready
      this.statusMatch = "inMatch";
    },
  },
};
</script>
