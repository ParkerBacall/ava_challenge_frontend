<template>
<div>
    <h1>Select a Conversation</h1>
    <div id="card-container">
        <div id='conversation-card' :key="conversation.id" v-for="conversation in conversations">
            <Conversation :conversation="conversation" v-on:del-conversation="$emit('del-conversation', conversation.id)"/>
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
    props: ["conversations"]
        
}
</script>

<style lang="css" scoped>
    #card-container{
        display: flex;
        justify-content: space-evenly;
        flex-wrap: wrap;
    }
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
</style>