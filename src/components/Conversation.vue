<template>
  <div>
     <h1>{{conversation.text}}</h1>
     <p>{{conversation.lastMutation}}</p>
  </div>
</template>

<script>
export default {
    name: "Conversation",
    props: ["conversation"]
}
</script>

<style>

</style>