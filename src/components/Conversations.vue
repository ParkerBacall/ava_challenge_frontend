<template>
<div>
    <div :key="conversation.id" v-for="conversation in conversations">
        <Conversation :conversation="conversation"/>
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

<style>

</style>