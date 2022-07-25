
<template>
  <div class="cell" v-on:click="toggle">
    <template>{{ text }}</template>
  </div>
</template>

<script>
import { getList } from './request';

export default {
  props: ["n"],

  data () {
    return {
      text: "",
    };
  },
  methods: {
    toggle () {
      if (this.text != "") {
        return;
      }
      this.text = this.n % 2 == 0 ? "x" : "o";
      this.$emit("cl", this.text);
      getList().then((res) => {
        console.log(res);
      });
    },
  },
};
</script>

<style>
.cell {
  border: 1px solid white;
  border-radius: 10px;
  width: 50px;
  text-align: center;
  font-size: 50px;
  line-height: 40px;
  padding-bottom: 10px;
  height: 40px;
  background-color: transparent;
  color: white;
}
</style>