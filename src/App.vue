<template>
  <h1>reaction timer</h1>
  <button @click="start" :disabled="isPlaying" >play</button>
  <Block v-if="isPlaying" :delay="delay" @end="endGame" />
  <p v-if="showResults">Reaction time: {{ score }} ms</p>
</template>

<script>
import { computed, ref } from '@vue/runtime-core'
import Block from './components/Block.vue'

export default {
  name: 'App',
  components:{
    Block
  },
  setup(){
    const isPlaying = ref(false)
    const delay = ref(null)
    const score = ref(null)
    const showResults = ref(false)

    const start = computed(() => {
      delay.value = 2000 + Math.random() * 5000
      isPlaying.value = true
      console.log(delay.value);
    })

    function endGame(reactionTime){
      score.value = reactionTime
      isPlaying.value = false
      showResults.value = true
    }

    return{
      isPlaying,
      delay,
      start,
      endGame,
      score,
      showResults
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
  color: #2c3e50;
  margin-top: 60px;
}
</style>
