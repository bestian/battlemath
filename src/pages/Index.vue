<template>
  <q-page>
    <div class="container">
      <q-linear-progress :value="time / 100" color="warning" class="q-mt-md" />
      <h4>您的分數:{{you}}</h4>
      <h4>敵人的分數:{{enemy}}</h4>
      <h3>{{n}} {{ type == 'p' ? '+' : '-'}} {{m}} = ?</h3>
      <q-input type="number" v-model="ans" @input = "check()"/>
      <q-btn color="primary" size ="xl" v-if = "win" @click="again()">你勝利了，按此重來</q-btn>
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  props: ['d'],
  data() {
    return {
      time: 0,
      you: 0,
      enemy: 0,
      n:3,
      m:4,
      ans: null,
      win: false,
      type: 'p'
    }
  },
  methods: {
    check() {
      if (this.type == 'p') {
        if (this.ans == this.n + this.m) {
          this.you++;
          this.time = 0;
          this.reset()
        }
      }
      if (this.type == 'm') {
        if (this.ans == this.n - this.m) {
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
      this.win = false
      this.reset()
    },
    reset() {
      this.type = ['p','m'][Math.floor(Math.random()*2)]
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
