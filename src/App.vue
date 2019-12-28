<template>
  <div id="app" class="container">
    <h2 class="title">井字棋</h2>
    <div class="wrapper">
      <div class="row">
        <cell @clickfn="fatherFn(0, $event)" :myNum="num" />
        <cell @clickfn="fatherFn(1, $event)" :myNum="num" />
        <cell @clickfn="fatherFn(2, $event)" :myNum="num" />
      </div>
      <div class="row">
        <cell @clickfn="fatherFn(3, $event)" :myNum="num" />
        <cell @clickfn="fatherFn(4, $event)" :myNum="num" />
        <cell @clickfn="fatherFn(5, $event)" :myNum="num" />
      </div>
      <div class="row">
        <cell @clickfn="fatherFn(6, $event)" :myNum="num" />
        <cell @clickfn="fatherFn(7, $event)" :myNum="num" />
        <cell @clickfn="fatherFn(8, $event)" :myNum="num" />
      </div>
      <div class="result">{{finFlag ? `获胜方: ${result}` : "胜负未定"}}</div>
    </div>
  </div>
</template>

<script>
import Cell from "./components/Cell.vue";

export default {
  name: "app",
  components: {
    Cell
  },
  data() {
    return {
      //计数
      num: 0,
      //二维数组
      map: [[null, null, null], [null, null, null], [null, null, null]],
      //结果
      result: "",
      //胜负开关
      finFlag: false,
    };
    //0 map[0][0]
    //1 map[0][1]
    //2 map[0][2]
    //3 map[1][0]
    //4 map[1][1]
    //5 map[1][2]
    //6 map[2][0]
    //7 map[2][1]
    //8 map[2][2]
  },
  methods: {
    fatherFn(i, text) {
        this.num += 1;
        this.map[Math.floor(i / 3)][i % 3] = text;
        this.win();
    },
    resetData() {
      this.map = [[null, null, null], [null, null, null], [null, null, null]];
      this.num = 0;
      this.result = '';
      this.finFlag = false;
    },
    win() {
      //横向相同
      for (let i = 0; i < 2; i++) {
        if (
          this.map[i][0] !== null &&
          this.map[i][0] === this.map[i][1] &&
          this.map[i][1] === this.map[i][2]
        ) {
          this.result = this.map[i][0];
          this.finFlag = true;
        }
      }
      //竖向相同
      for (let j = 0; j < 2; j++) {
        if (
          this.map[0][j] !== null &&
          this.map[0][j] === this.map[1][j] &&
          this.map[1][j] === this.map[2][j]
        ) {
          this.result = this.map[0][j];
          this.finFlag = true;
        }
      }
      //斜向相同
      if (
        this.map[0][0] !== null &&
        this.map[0][0] === this.map[1][1] &&
        this.map[1][1] === this.map[2][2]
      ) {
        this.result = this.map[0][0];
        this.finFlag = true;
      }
      if (
        this.map[0][2] !== null &&
        this.map[0][2] === this.map[1][1] &&
        this.map[1][1] === this.map[2][0]
      ) {
        this.result = this.map[0][2];
        this.finFlag = true;
      }
    }
  }
};
</script>

<style>
.container {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center;
  color: #2c3e50;
  margin-top: 60px; */
  display: flex;
  flex-direction: column;
  align-items: center;
}
.row {
  display: flex;
}
</style>
