<template>
  <div class="hello">
    <h1>
      Let's send
      <input type="number" min="0" v-model="inputNum"> resumes!
    </h1>

    <p>{{cellsNum}}</p>
  </div>
</template>

<script>
export default {
  name: "Header",
  props: {
    cellsNum: String
  },
  model: {
    props: "cellsNum",
    event: "input"
  },
  computed: {
    inputNum: {
      get() {
        return this.cellsNum;
      },
      set(value) {
        this.$emit("input", value);
      }
    }
  }
};
</script>


<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
