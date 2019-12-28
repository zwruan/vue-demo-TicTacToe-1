<template>
  <div class="cell" @click="myClick()">
    <template v-if="showFlag">{{text}}</template>
    <template v-else></template>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showFlag: false,
      text: "",
    };
  },
  props: ["myNum"],
  methods: {
    myClick() {
      if (this.text !== "") {
        return;
      }
      this.showFlag = true;
      this.text = this.myNum % 2 === 0 ? "x" : "o";
      this.$emit("clickfn", this.text);
    }
  }
};
</script>

<style>
.cell {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100px;
  height: 100px;
  border: 1px solid #000;
  box-sizing: border-box;
  font-size: 80px;
}
</style>