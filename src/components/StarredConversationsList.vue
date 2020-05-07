<template>
  <div id="card-container">

      <div  
      :key="conversation.id"  
      v-for="conversation in starredConversations">

        <Conversation :conversation="conversation"
        v-on:toggle-show="$emit('toggle-show', conversation)"
        :starredConversations="starredConversations"
        v-on:unstar-conversation="$emit('unstar-conversation', conversation)"
        />
      </div>
  </div>
</template>

<script>
import Conversation from "./Conversation"
export default {
name: 'StarredConversationsList',
components: {
  Conversation
},
props: ["starredConversations"]
}
</script>

<style lang="css" scoped>
    #card-container{
        display: flex;
        justify-content: space-evenly;
        flex-wrap: wrap;
    }
</style>