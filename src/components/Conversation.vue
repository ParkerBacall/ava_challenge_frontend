<template>
  <div>
     <h2>{{conversation.text}}</h2>
     <button v-on:click="$emit('del-conversation', conversation.id)">Delete</button>
     <button>Star</button>
  </div>
</template>

<script>
export default {
    name: "Conversation",
    props: ["conversation"]
}
</script>

<style lang="sass" scoped>
    
</style>