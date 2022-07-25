<template>
  <div class="box" @click="test" @keyup.enter="test">
    <div class="title">第{{ n }}手</div>
    <div class="row">
      <cell ref="cellOne" @cl="s(0, $event)" :n="n" />
      <cell @cl="s(1, $event)" :n="n" />
      <cell @cl="s(2, $event)" :n="n" />
    </div>
    <div class="row">
      <cell @cl="s(3, $event)" :n="n" />
      <cell @cl="s(4, $event)" :n="n" />
      <cell @cl="s(5, $event)" :n="n" />
    </div>
    <div class="row">
      <cell @cl="s(6, $event)" :n="n" />
      <cell @cl="s(7, $event)" :n="n" />
      <cell @cl="s(8, $event)" :n="n" />
    </div>
    <!-- <footer>{{ flag == false ? `胜负未分` : `胜者是${text}` }}</footer> -->
    <footer v-if="flag">胜者是{{ text }}</footer>
    <footer v-else>胜负未分</footer>
  </div>
</template>

<script>
import Cell from "./Cell.vue";

export default {
  components: {
    Cell,
  },
  data () {
    return {
      n: 0,
      arr: [[], [], []],
      flag: false,
      text: ``,
    };
  },
  mounted () {
    console.log('refs ===>', this.$refs,
      'refs.cellOne', this.$refs.cellOne);
  },
  methods: {
    s (i, text) {
      this.n++;
      this.arr[Math.floor(i / 3)][i % 3] = text;
      this.flag ? `` : (this.text = text);
      this.tell();
    },
    test () {
      console.log('click');
    },
    test1 () {
      console.log('enter')
    },
    tell () {
      const arr = this.arr;

      for (let i = 0; i < 3; i++) {
        if (
          (arr[i][0] && arr[i][0] == arr[i][1] && arr[i][1] == arr[i][2]) ||
          (arr[0][i] && arr[0][i] == arr[1][i] && arr[1][i] == arr[2][i]) ||
          (arr[1][1] &&
            ((arr[1][1] == arr[0][0] && arr[1][1] == arr[2][2]) ||
              (arr[1][1] == arr[0][2] && arr[1][1] == arr[2][0])))
        ) {
          this.flag = true;
        }
      }
    },
  },
};
</script>

<style>
:root {
  width: fit-content;
  margin: 0 auto;
}

.title {
  text-align: center;
  color: azure;
  margin: 5px;
  font-size: 20px;
}

footer {
  margin-top: 5px;
  color: aliceblue;
  text-align: center;
}

.row {
  display: flex;
}

.row .cell {
  margin: 5px;
}
</style>
