<template>
<div class="gameResult" :class="{fast: isFast}">
  <p>Reaction Time: {{result}} ms </p>
  <p :class="{rankResult: score <= 150}"> {{rank}} </p>
</div>
</template>

<script>
export default {
    props: ['result'],
    data(){
        return {
            rank: '',
            score: this.result,
            isFast: false
        }
    },
    mounted(){
        if(this.result > 1500){
            this.rank = `You are really slow! like a snail`
        } else if(this.result > 1000){
            this.rank = `Uhh, you could do better`
        } else if (this.result > 500){
            this.rank = `Wow, you are fast, but not the fastest`
            this.isFast = true
        } else {
            this.rank = `Impressive, The Flash!`
            this.isFast = true
        }
    },
    unmounted(){
        this.isFast = false
        console.log(`Result unmonted!`)
    }
}
</script>

<style>
.gameResult{
    background: rgba(129, 45, 45, 0.5);
    border-radius: 25px;
    width: 400px;
    margin: auto;
    padding: 10px;
    margin-top: 20rem;
    color: white;
    font-size: 1.3rem;
    z-index: 100;
}
.fast{
    background: rgba(56, 122, 56, 0.5);
}
.rankResult{
    color: white;
    font-size: 2rem;
}
</style>