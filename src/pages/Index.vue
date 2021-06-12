<template>
  <q-page>
    <div class="container">
      <q-linear-progress :value="time / 100" color="warning" class="q-mt-md" />
      <h4><q-img src="../assets/you.png" 
      spinner-color="white"
      style="height: 100px; max-width: 100px"/> 您的分數:{{you}}</h4>
      <h4><q-img src="../assets/enemy.png" 
      spinner-color="white"
      style="height: 100px; max-width: 100px"/>敵人的分數:{{enemy}}</h4>
      <h3>{{n}} {{ type }} {{m}} = ?</h3>
      <q-input type="number" v-model="ans" @input = "check()"  
        label="您的答案"/>
      <q-btn color="primary" size ="xl" v-if = "win" @click="again()">你勝利了，按此重來</q-btn>
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  props: ['d', 'types'],
  data() {
    return {
      time: 0,
      you: 0,
      enemy: 0,
      n:3,
      m:4,
      ans: null,
      win: false,
      type: '+'
    }
  },
  methods: {
    check() {
      if (this.type == '+') {
        if (this.ans == this.n + this.m) {
          this.you++;
          this.time = 0;
          this.reset()
        }
      }
      if (this.type == '-') {
        if (this.ans == this.n - this.m) {
          this.you++;
          this.time = 0;
          this.reset()
        }
      }
      if (this.type == '×') {
        if (this.ans == this.n * this.m) {
          this.you++;
          this.time = 0;
          this.reset()
        }
      }
      if (this.you > this.enemy + 10) {
        this.win = true
      }
    },
    again() {
      this.you = 0
      this.enemy = 0
      this.time = 0
      this.win = false
      this.reset()
    },
    reset() {
      this.type = this.types[Math.floor(Math.random()*this.types.length)]
      this.n = Math.floor(Math.random()*this.d) + this.d + 1;
      this.m = Math.floor(Math.random()*this.d) + 1;
      this.ans = null;
    },
    go() {
      this.time++;
      if (this.time >= 100) {
        this.enemy++
        this.reset()
        this.time = 0
      }
    }
  },
  mounted() {
    this.reset()
    setInterval(this.go, 100)
  }
}
</script>

<style type="text/css" scoped="">
  .container {
    max-width: 620px;
    margin: 0 auto;
  }
</style>
