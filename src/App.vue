<template>
  <div id="app">

    <button v-if="!this.show && !this.showStars" v-on:click="toggleStar">View Starred Conversations</button>
    <button  v-if="this.showStars && !this.show" v-on:click="toggleStar">Show all Conversations</button>

    <ShowConversation v-if="this.show" 
    :conversation="selectedConversation"
     v-on:toggle-show="toggleShow"
    />

    <Conversations v-if="!this.show && !this.showStars" :conversations="conversations" 
    v-on:del-conversation="deleteConvo"
    v-on:star-conversation="starConvo"
    v-on:unstar-conversation="unstarConvo"
    :starredConversations="starredConversations"
    v-on:toggle-show="toggleShow"
    />

    <StarredConversationsList 
    v-if="this.showStars && !this.show"
    :starredConversations="starredConversations"
    v-on:unstar-conversation="unstarConvo"
    v-on:toggle-show="toggleShow"
    />

  </div>
</template>

<script>
import Conversations from './components/Conversations'
import ShowConversation from './components/ShowConversation'
import StarredConversationsList from './components/StarredConversationsList'
export default {
  name: 'App',
  components: {
    Conversations,
    ShowConversation,
    StarredConversationsList
  },
   data(){
        return {
          conversations: [],
          show: false,
          selectedConversation: {},
          starredConversations: [],
          showStars: false
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
    },
    starConvo(conversation){
      event.stopPropagation();
      if  (!this.starredConversations.includes(conversation)){
      this.starredConversations = [...this.starredConversations, conversation]
      }
    },
    toggleStar(){
      this.showStars = !this.showStars
    },
    unstarConvo(conversation){
       event.stopPropagation();
      this.starredConversations = this.conversations.filter(convo => convo != conversation)
    }
    },
    mounted(){
        fetch('http://localhost:9001/conversations')
        .then(response => response.json())
        .then(response => {
          response.conversations.map(conversation => {
            this.conversations = conversation
          })
        })
    }
}

</script>

<style scoped>
  
</style>
