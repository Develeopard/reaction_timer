<template>
  <div v-if="showBlock" @click="stopTimer" class="block">
      click me
  </div>
</template>

<script>
import { onMounted,  ref } from '@vue/runtime-core'
export default {
    props: ['delay'],
    setup(props, context){
        const showBlock = ref(false)
        const timer = ref(null)
        const reactionTime = ref(0)

        const startTimer = () => {
            setInterval(() => {
                reactionTime.value += 10
            }, 10)
        }

        const stopTimer = () => {
            clearInterval(timer.value)
            context.emit('end', reactionTime.value)
            console.log(reactionTime.value);
        }

        onMounted(() => {
            console.log('component mounted');
            setTimeout(() => {
                showBlock.value = true
                startTimer()
            }, props.delay)
        })

        return{
            showBlock,
            timer,
            reactionTime,
            stopTimer
        }
    },


}
</script>

<style>
    .block{
        width: 400px;
        border-radius: 20px;
        background: #0faf87;
        color: white;
        text-align: center;
        padding: 100px 0;
        margin: 40px auto;
    }
</style>