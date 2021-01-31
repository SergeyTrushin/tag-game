<template>
  <div>
    <h1>Пятнашки</h1>
    <hr>
    <button @click="startGame" :class="{start: !start, stop: start}" class="btn">{{start ? 'Стоп' : 'Старт'}}</button>
    <button class="btn" @click="almostWinSort">TEST BUTTON</button>
    <span>Ходов: {{steps}}</span>
    <span>Время: {{m}}:{{s}}</span>
    <div class="fild">
      <div v-for="(cell, i) of map" :key="i" class="cell"   @click="move(cell)" :class="{'zero': cell == 0}">
        {{cell == 0 ? '' : cell}}
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    methods: {
      startGame() {
        if (this.start) {
          this.stopGame();
        } else {
          this.startTimer();
          let arr = this.getRandomarray();
          this.map = arr;
          this.start = true;
        }
      },
      stopGame() {
        this.start = false;
        this.sortMap();
        this.steps = 0;
        this.m = 0;
        this.s = 0;
        clearInterval(this.timer);
      },
      almostWinSort() {
        if (this.start) {
          this.map = [1,2,3,4,5,6,7,8,9,10,11,12,13,14,0,15]
        }
      },
      sortMap() {
        this.map.sort((a,b) => {
          if (a < b) return -1;
          if (a > b) return 1;
          if (a == b) return 0;
        })
        this.map.push(0);
        this.map.shift()
      },
      startTimer(str) {
        this.timer = setInterval(()=>{
          this.s++;
          if (this.s > 59) {
            this.s = 0;
            this.m ++;
          }
        }, 1000)
      },
      move(id) {
        if (this.start) {
          const zeroIndex = this.map.indexOf(0);
          const cellIndex = this.map.indexOf(id);
          if (cellIndex - 4 == zeroIndex || cellIndex + 4 == zeroIndex || cellIndex + 1 == zeroIndex || cellIndex - 1 == zeroIndex) {
            this.map[zeroIndex] = id;
            this.map[cellIndex] = 0;
            this.steps++;
          }
          this.map.push(0);
          this.map.pop();

          this.checkWin();
        }
      },
      checkWin() {
        let test = true;
        for (let i = 0; i < this.map.length-1; i++) {
          if (this.map[i] !== i + 1) {
            test = false;
          }
        }

        if (test == true) {
          console.log(this.map);
          this.stopGame();
        }
      },
      getRandomarray() {
        let array = [];
        while (array.length < 16) {
          let number = this.getRandomIntInclusive(0, 15);
          if (array.indexOf(number) == -1) {
            array.push(number)
          }
        }
        return array
      },
      getRandomIntInclusive(min, max) {
        min = Math.ceil(min);
        max = Math.floor(max);
        return Math.floor(Math.random() * (max - min + 1)) + min;
      }
    },
    data() {
      return {
        map: [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,0],
        start: false,
        steps: 0,
        win: false,
        m: 0,
        s: 0,
        timer: null,
      }
    }
  }
</script>

<style lang="less">
  .btn{
    border: none;
    border-radius: 5px;
    padding: 10px 5px;
    display: flex;
    justify-content: center;
    align-items: center;
    min-width: 150px;
    margin: 10px auto;
    outline: none;
    background: #ccc;
    &.start{
      background: #51e898;
      color: #fff;
    }
    &.stop{
      background: red;
      color: #fff;
    }
  }

  .fild{
    width: 408px;
    height: 408px;
    margin: 10px auto 0;
    background: #fff;
    border: 1px solid;
    display: flex;
    flex-wrap: wrap;
    box-sizing: content-box;
    .cell{
      border: 1px solid;
      width: 100px;
      height: 100px;
      margin:1px;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 30px;
      font-weight: bold;
      cursor: pointer;
      &:hover{
        background:#ccc;
      };
      &:active{
        background:#ccc;
        color: yellow;
      };
      &.zero{
        background: grey;
      }
    }
  }
</style>
