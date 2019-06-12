<template>
  <div>
    <div v-for="cells in makeCells">
      <div>a</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Cells",
  props: {
    updatedCellsNum: String
  },
  computed: {
    makeCells() {
      const num = parseInt(this.updatedCellsNum);
      const arr = [...Array(num).keys()];
      return arr;
    }
  }
};
</script>