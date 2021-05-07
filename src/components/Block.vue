<template>
  <div class="block" v-if="showBlock" @click="stopTimer">
      <p>Click Me</p>
  </div>
</template>

<script>
export default {
    props: ['delay'],
    data(){
        return{
            showBlock: false,
            timer: null,
            resultTime: 0
        }
    },
    mounted(){
        setTimeout(()=> {
            this.showBlock = true
            this.startTimer()
        }, this.delay)
    },
    methods: {
        startTimer(){
            this.timer = setInterval( () => {
                this.resultTime += 10
            }, 10)
        },
        stopTimer(){
            clearInterval(this.timer)
            this.$emit('result', this.resultTime)
        }
    }
}
</script>

<style>
.block{
    background: antiquewhite;
    color: crimson;
    border-radius: 50%;
    text-align: center;
    width: 10rem;
    height: 5rem;
    margin: auto;
    padding: 30px 0;
    display: flex;
    align-items: center;
    justify-content: center;
}

p{
    font-size: 1.5rem;
}
</style>