<template>
  <div class="container">
    <h1>Timer Game - Speed Test</h1>
    <p>Let`s see just how fast you are!</p>
    <button @click="startPlaying" :disabled="isPlaying">Play</button>
  </div>
  <div ref="block" id="playBlock">
    <Block v-if="isPlaying" :delay="delay" @result="showResult" />
  </div>
  <!-- <p>Reaction Time: {{ score }} ms</p> -->
  <Result v-if="displayResult" :result="score"/>
  <div class="circle" id="circle-top-left"></div>
  <div class="circle" id="circle-top-right"></div>
  <div class="circle" id="circle-bottom-left"></div>
  <div class="circle" id="circle-bottom-right"></div>
</template>

<script>

import Block from './components/Block.vue'
import Result from './components/Result.vue'

export default {
  name: 'App',
  components: {
    Block, Result
  },
  data(){
    return {
      isPlaying: false,
      delay: null,
      displayResult: false,
      score: null,
      minWidth: window.innerWidth,
      minHeight: window.innerHeight,
    }
  },
  methods: {
    startPlaying(){
      this.placeBlock()
      this.delay = 2000 + Math.random() * 5000
      this.isPlaying = true
      this.displayResult = false
      console.log(this.delay)
    },
    showResult(result){
      console.log(`this is the emit result`, result);
      this.score = result;
      this.isPlaying = false
      this.displayResult = true     
    },
    randomPosition(min, max){
        return Math.random() * (max - min) + min;
    },
    placeBlock(){
        console.log(this.$refs.play)
        this.$refs.block.style.top = this.randomPosition(0, this.minHeight)+"px"
        this.$refs.block.style.left = this.randomPosition(0, this.minWidth)+"px"
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: crimson;
  margin-top: 60px;
}

body{
  background-color: black;
  max-height: 100vh;
  overflow: hidden;
}
.container{
  position: relative;
  /* background: lightgreen; */
  top: 25vh;

}
.container h1{
  font-size: 3rem;
}

.container button{
  padding: 1rem;
  width: 10rem;
  margin: auto;
  border-radius: 25px;
  outline: none;
  border: none;
  font-size: 1.5rem;
  font-weight: bold;
  margin-top: 2rem;
}

#playBlock{
  position: absolute;
  z-index: 1;
}

.circle{
  border-radius: 50%;
  width: 600px;
  height: 600px;
  background: crimson;
  position: absolute;
}

#circle-top-left{
  top: 0;
  left: 0;
  transform: translate(-70%, -50%);
}

#circle-top-right{
  top: 0;
  right: 0;
  transform: translate(70%, -50%);
}

#circle-bottom-left{
  bottom:  0;
  right: 0;
  transform: translate(70%, 50%);
}

#circle-bottom-right{
  bottom:  0;
  left: 0;
  transform: translate(-70%, 50%);
}
</style>
