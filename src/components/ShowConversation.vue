<template>
  <div>
      <button v-on:click="$emit('toggle-show', conversation)">back</button>
      <h3>{{conversation.text}}</h3>
      <p>{{conversation.lastMutation}}</p>
  </div>
</template>

<script>
export default {
    name: "ShowConversation",
    props: ["conversation", "starredConversations"]
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