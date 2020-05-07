<template>
  <div id="app">

    <button v-if="!this.show && !this.showStars" v-on:click="toggleStar">View Starred Conversations</button>
    <button  v-if="this.showStars && !this.show" v-on:click="toggleStar">Show all Conversations</button>

    <ShowConversation v-if="this.show" 
    :conversation="selectedConversation"
     v-on:toggle-show="toggleShow"
    />

    <AddConversation
    v-if="!this.show && !this.showStars"
    v-on:add-convo="postConvo"
    />

    <Conversations v-if="!this.show && !this.showStars" :conversations="conversations" 
    v-on:del-conversation="deleteConvo"
    v-on:star-conversation="starConvo"
    v-on:unstar-conversation="unstarConvo"
    :starredConversations="starredConversations"
    v-on:toggle-show="toggleShow"
    />

    <AddMutations
      v-if="this.show"
      v-on:add-mutation="postMutation"
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
import AddConversation from "./components/AddConversation"
import AddMutations from "./components/AddMutation"
import Conversations from './components/Conversations'
import ShowConversation from './components/ShowConversation'
import StarredConversationsList from './components/StarredConversationsList'
export default {
  name: 'App',
  components: {
    Conversations,
    ShowConversation,
    StarredConversationsList,
    AddConversation,
    AddMutations
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
      this.starredConversations = this.starredConversations.filter(convo => convo != conversation)
    },
    postConvo(newConvo){
      fetch('http://localhost:9001/mutations',{
        method: 'POST',
        headers:{
          'content-type': 'application/json'
        },
        body: JSON.stringify({
          "author": newConvo.author,
          "conversationId": '_' + Math.random().toString(36).substr(2, 9),
          data:{
            "index": 0,
            "length": newConvo.text.length,
            "type": "insert",
            "text": newConvo.text,
          },
          origin:{
            "alice": newConvo.author === 'Alice' ? 1 : 0,
            "bob": newConvo.author === 'Bob' ? 1 : 0
          }
        })
      })
      .then(response => response.json())
      .then(convo => this.conversations = [...this.conversations, convo[0]])
    },
    postMutation(newMutation){
      fetch('http://localhost:9001/mutations',{
        method: 'POST',
        headers:{
          'content-type': 'application/json'
        },
        body: JSON.stringify({
          "author": newMutation.author,
          "conversationId": this.selectedConversation.id,
           "data": {
            "index": this.selectedConversation.text.length,
            "length": newMutation.text.length,
            "type": "insert",
            "text": newMutation.text,
           },
           origin: {
          "alice": newMutation.author === 'Alice' ? 1 : 0,
          "bob": newMutation.author === 'Bob' ? 1 : 0
           }
        })
      })
      .then(response => response.json())
      .then(mutation => {
        this.selectedConversation.lastMutation = mutation[0]
        this.selectedConversation.text = `${this.selectedConversation.text} ${ mutation[0].text}`
        })
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
