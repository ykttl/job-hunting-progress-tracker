<template>
  <div class="container">
    <div class="cellsContainer">
      {{updatedCellsNum}}
      <template
        v-for="(resume, index) in resumeData"
        v-if="index < updatedCellsNum"
      >
        <div class="cell" :key="resume.number">
          {{resume.number}}
          <div v-if="editing === resume.number">
            <input type="text" v-model="resume.company" class="editing">
            <input type="text" v-model="resume.howToApply" class="editing">
            <input type="text" v-model="resume.status" class="editing">
            <input type="text" v-model="resume.appliedDate" class="editing">
            <button @click="savesave(resume)">save</button>
            <button @click="cancelEdit(resume)">Cancel</button>
          </div>

          <div v-else>
            <p>{{resume.company}}</p>
            <p>{{resume.status}}</p>
            <p>{{resume.howToApply}}</p>
            <p>{{resume.appliedDate}}</p>
            <button @click="editMode(resume)">edit</button>
          </div>
        </div>
      </template>
    </div>
  </div>
</template>

<script>
export default {
  name: "Cells",
  props: {
    updatedCellsNum: String,
    resumeData: Array,
    dataFromServer: Array
  },
  data() {
    return {
      editing: null
    };
  },
  methods: {
    editMode(resume) {
      //ここでデータオブジェクトつくる？
      this.cachedData = Object.assign({}, resume);
      this.editing = resume.number;
    },
    cancelEdit(resume) {
      console.log(resume);
      Object.assign(resume, this.cachedData);
      this.editing = null;
    },
    savesave(resume) {
      this.$emit("save:savesave", resume.number, resume);
      this.editing = null;
    }
  },
  computed: {}
};
</script>

<style scoped>
.container {
  width: 60%;
  margin: 0 auto;
}
.cellsContainer {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}
.cell {
  margin: 30px;
}
.editing {
  display: block;
}
</style>
