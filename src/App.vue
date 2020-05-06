<template>
  <div id="app">
    <Conversations :conversations="conversations"/>
  </div>
</template>

<script>
import Conversations from './components/Conversations'
export default {
  name: 'App',
  components: {
    Conversations
  },
   data(){
        return {
          conversations: [],

        }
    },
    mounted(){
        fetch('http://localhost:9001/conversations')
        .then(response => response.json())
        .then(conversations => {
          this.conversations = conversations
        })
    }
}
</script>

<style>

</style>
