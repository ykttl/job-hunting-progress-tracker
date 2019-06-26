<template>
  <div id="app">
    <Header v-model="cellsNum"/>
    <Cells
      :resumeData="resumeData"
      :updatedCellsNum="updatedCellsNum"
      :dataFromServer="dataFromServer"
      @save:savesave="savesave"
    />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Cells from "./components/Cells.vue";
import { close, closeSync } from "fs";
import { clearLine } from "readline";

export default {
  name: "app",
  components: {
    Header,
    Cells
  },
  data() {
    return {
      cellsNum: 0,
      resumeData: [],
      dataFromServer: []
    };
  },
  mounted() {
    //this.getServerData();
  },
  updated() {
    this.createCells();
    // this.getServerData();
  },
  methods: {
    async getServerData() {
      const datadata = await localStorage.getItem("apple");
      if (datadata) {
        this.dataFromServer = JSON.parse(datadata);
      }
      console.log("state", this.dataFromServer);
    },

    async savesave(id, resume) {
      let dataFromLocal = await JSON.parse(localStorage.getItem("apple"));
      let dataToSave;

      if (dataFromLocal) {
        dataFromLocal = dataFromLocal.filter(item => item.number !== id);
        dataToSave = [...dataFromLocal, resume];
      } else {
        dataToSave = [resume];
      }
      localStorage.setItem("apple", JSON.stringify(dataToSave));
      this.getServerData();
    }
  },
  computed: {
    updatedCellsNum() {
      return this.cellsNum;
    },
    createCells() {
      // this.getServerData();
      const arr = [];
      const num = parseInt(this.cellsNum);
      for (let i = 0; i < num; i++) {
        arr.push({
          number: i + 1,
          company: "",
          status: "",
          howToApply: "",
          appliedDate: "",
          interview: {
            phone: 0,
            skype: 0,
            inPerson: 0,
            technicalExam: 0
          },
          note: ""
        });
      }
      this.resumeData = arr;

      // const newnew = this.resumeData.map(resumeItem => {
      //   this.dataFromServer.map(serverItem => {
      //     if (resumeItem.number === serverItem.number) {
      //       console.log("haaaa");
      //       resumeItem = serverItem;
      //     }
      //   });
      // });

      // this.resumeData = newnew;

      console.log(this.resumeData);
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
