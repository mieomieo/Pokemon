<template>
  <h1>Congratulations</h1>
  <p>{{ Math.round(timer / 1000) }} second</p>
  <button @click="onStartAgain">Start Again</button>
</template>
<script>
export default {
  props: {
    timer: {
      type: Number,
      required: true,
    },
  },
  methods: {
    onStartAgain() {
      this.$emit("onStartAgain");
    },
  },
};
</script>
