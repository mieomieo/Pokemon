<template>
  <div class="screen">
    <h1>Interact Component here...</h1>
    <card-flip
      v-for="(card, index) in cardsContext"
      :key="index"
      :ref="`card-${index}`"
      :imgBackFaceURL="`images/${card}.png`"
      :card="{ index, value: card }"
      @onFlip="checkRule($event)"
    />
  </div>
</template>
<script>
import CardFlip from "./CardPokemon.vue";
export default {
  data() {
    return {
      rules: [],
    };
  },
  props: {
    cardsContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  components: {
    CardFlip,
  },

  methods: {
    checkRule(card) {
      // console.log(card);
      if (this.rules.length === 2) return false;
      this.rules.push(card);
      // console.log(this.rules);
      if (
        this.rules.length === 2 &&
        this.rules[0].value === this.rules[1].value
      ) {
        // add class 'disable ' to component card
        console.log("Right");
        this.$refs[`card-${this.rules[0].index}`][0].onEnableDisableMode();
        this.$refs[`card-${this.rules[1].index}`][0].onEnableDisableMode();
        // reset rules to []
        this.rules = [];
        const disabledElements = document.querySelectorAll(
          ".screen .card.disabled"
        );
        console.log(disabledElements);
        if (
          disabledElements &&
          disabledElements.length === this.cardsContext.length - 2
        ) {
          setTimeout(() => {
            this.$emit("onResult");
            console.log("RESULT");
          }, 920);
        }
      } else if (
        this.rules.length === 2 &&
        this.rules[0].value !== this.rules[1].value
      ) {
        console.log("Wrong");
        // console.log(this.$refs);
        let temp = [...this.rules];
        console.log("temp:", temp);
        let index0 = this.rules[0].index;
        let index1 = this.rules[1].index;
        this.rules = [];

        // temp = [];
        console.log("this.rules:", this.rules);

        setTimeout(() => {
          // close two cards
          // console.log(this.$refs[`card-${this.rules[0].index}`]);
          this.$refs[`card-${index1}`][0].onFlipBackCard();
          this.$refs[`card-${index0}`][0].onFlipBackCard();

          // reset rules to []
          this.temp = [];
        }, 800);
      } else return false;
    },
  },
};
</script>
