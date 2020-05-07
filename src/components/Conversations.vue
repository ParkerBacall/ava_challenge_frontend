<template>
<div>
    <h1>Select a Conversation</h1>
    <div id="card-container">
        <div :key="conversation.id" v-for="conversation in conversations">
            <Conversation 
            :conversation="conversation" 
            :starredConversations="starredConversations"
            v-on:del-conversation="$emit('del-conversation', conversation.id)"
            v-on:star-conversation="$emit('star-conversation', conversation)"
            v-on:unstar-conversation="$emit('unstar-conversation', conversation)"
            v-on:toggle-show="$emit('toggle-show', conversation)"
            />
    </div>
    </div>
</div>
</template>

<script>
import Conversation from "./Conversation"
export default {
    name: "Conversations",
    components: {
        Conversation
    },
    props: ["conversations","starredConversations"]
        
}
</script>

<style lang="css" scoped>
    #card-container{
        display: flex;
        justify-content: space-evenly;
        flex-wrap: wrap;
    }
   
</style>