<template>
  <h2>Reaction time: {{ score }} ms</h2>
  <p class="rank">{{ rank }}</p>
</template>

<script>
import { ref } from '@vue/reactivity'
import { onMounted } from '@vue/runtime-core'
export default {
    props: ['score'],
    setup(props){
        const rank = ref(null)

        onMounted(() => {
            if(props.score < 250){
                rank.value = 'Fast'
            }else if(props.score < 400){
                rank.value = 'Moderate'
            }else{
                rank.value = 'Slow'
            }

            console.log('rank mounted');
        })

        return{
            rank,
        }
    }
    }
</script>

<style>

</style>