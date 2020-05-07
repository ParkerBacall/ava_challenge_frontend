<template>
  <div :id="starredConversations.includes(conversation) ? 'starred' : 'conversation-card'" 
  v-on:click="$emit('toggle-show', conversation)">
     <h2>{{conversation.text}}</h2>
     <button v-on:click="$emit('del-conversation', conversation.id)">Delete</button>
     <button v-if="!starredConversations.includes(conversation)" v-on:click="$emit('star-conversation', conversation)">Star</button>
     <button v-else v-on:click="$emit('unstar-conversation', conversation)">Un-star</button>
  </div>
</template>

<script>
export default {
    name: "Conversation",
    props: ["conversation","starredConversations"]
}
</script>

<style scoped>
 #conversation-card{
        width: 250px;
        height: 100px;
        padding:10px;
        border-radius:10px;
        margin:10px;
        box-shadow: 0px 0px 4px #666;
    }
    #conversation-card:hover{
        background-color: #999;
        width: 250px;
        height: 100px;
        padding:10px;
        border-radius:10px;
        margin:10px;
        box-shadow: 0px 0px 4px #666;
    }
    #starred{
        width: 250px;
        height: 100px;
        padding:10px;
        border-radius:10px;
        margin:10px;
        background-color: goldenrod;
        box-shadow: 0px 0px 4px #666;
    }
</style>