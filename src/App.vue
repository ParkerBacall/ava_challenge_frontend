<template>
  <div id="app">
    <Conversations :conversations="conversations" v-on:del-conversation="deleteConvo"/>
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
    methods: {
      deleteConvo(id){
      this.conversations = this.conversations.filter(conversation => conversation.id != id)
      fetch(`http://localhost:9001/conversations/${id}`, {
        method: 'DELETE'
      })
      .then(res => res.json())
      .then(console.log)
      .catch(err => console.log(err))
    },
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

<style scoped>
  
</style>
