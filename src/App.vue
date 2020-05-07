<template>
  <div id="app">
    <ShowConversation v-if="this.show" 
    :conversation="selectedConversation"
     v-on:toggle-show="toggleShow"
    />

    <Conversations v-else :conversations="conversations" 
    v-on:del-conversation="deleteConvo"
    v-on:toggle-show="toggleShow"
    />
  </div>
</template>

<script>
import Conversations from './components/Conversations'
import ShowConversation from './components/ShowConversation'
export default {
  name: 'App',
  components: {
    Conversations,
    ShowConversation
  },
   data(){
        return {
          conversations: [],
          show: false,
          selectedConversation: {}
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
    toggleShow(conversation){
      this.selectedConversation = conversation
      this.show = !this.show
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

<style scoped>
  
</style>
