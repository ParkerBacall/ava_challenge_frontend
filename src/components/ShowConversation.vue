<template>
  <div>
      <button v-on:click="$emit('toggle-show', conversation)">back</button>
      {{conversation}}
  </div>
</template>

<script>
export default {
    name: "ShowConversation",
    props: ["conversation"]
}
</script>

<style>

</style>