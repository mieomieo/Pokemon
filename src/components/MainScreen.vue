<template>
  <h1>POKE MEMMORIES</h1>
  <h2>Select mode</h2>
  <div class="select-container">
    <div class="actions">
      <button @click="onStart(16)">
        <span>4x4</span>
        <p>Easy</p>
      </button>
      <button @click="onStart(36)">
        <span>6x6</span>
        <p>Normal</p>
      </button>
      <button @click="onStart(64)">
        <span>8x8</span>
        <p>Hard</p>
      </button>
      <button @click="onStart(100)">
        <span>10x10</span>
        <p>Very Hard</p>
      </button>
    </div>
  </div>
</template>
<script>
export default {
  methods: {
    onStart(totalOfBlocks) {
      this.$emit("onStart", { totalOfBlocks });
    },
  },
};
</script>
<style>
h1 {
  font-size: 60px;
  text-align: center;
  margin-bottom: 30px;
  margin-top: 50px;
}
h2 {
  text-align: center;
  margin-bottom: 15%;
}
.select-container {
  /* width: 100%; */
}
.select-container .actions {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
.select-container .actions button {
  padding: 30px;
  border-radius: 10px;
  margin-right: 5%;
  background-color: #3ec6cf;
  color: aliceblue;
  font-size: 20px;
}
</style>
