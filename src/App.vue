<template>
  <main-screen
    v-if="statusMatch === 'default'"
    @onStart="onHandleBeforeStart($event)"
  />
  <interact-screen
    v-if="statusMatch === 'match'"
    :cardsContext="settings.cardsContext"
    @onResult="onResultScreen"
  />
  <result-screen
    :timer="timer"
    v-if="statusMatch === 'result'"
    @onStartAgain="this.statusMatch = 'default'"
  />
</template>
<script>
import MainScreen from "./components/MainScreen.vue";
import InteractScreen from "./components/InteractScreen.vue";
import { shuffled } from "@/utils/array.js";
// import { time } from "console";
import ResultScreen from "./components/ResultScreen.vue";
// import CopyRight from "./components/CopyRight.vue";

export default {
  name: "App",
  components: {
    MainScreen,
    InteractScreen,
    ResultScreen,
    // CopyRight,
  },
  data() {
    return {
      settings: {
        totalOfBlock: 0,
        cardsContext: [],
        startedAt: null,
      },
      statusMatch: "default",
      timer: 0,
    };
  },
  methods: {
    onResultScreen() {
      //get timer
      console.log(this.settings.startedAt);
      this.timer = new Date().getTime() - this.settings.startedAt;
      this.statusMatch = "result";
    },
    onHandleBeforeStart(config) {
      console.log("running handle before start ", config);
      this.settings.totalOfBlock = config.totalOfBlocks;
      const firstCards = Array.from(
        { length: this.settings.totalOfBlock / 2 },
        (_, i) => i + 1
      );
      const secondCards = [...firstCards];
      const cards = [...firstCards, ...secondCards];
      this.settings.cardsContext = shuffled(shuffled(shuffled(cards)));
      console.log(this.settings.cardsContext);
      this.settings.startedAt = new Date().getTime();

      this.statusMatch = "match";
    },
  },
};
</script>
