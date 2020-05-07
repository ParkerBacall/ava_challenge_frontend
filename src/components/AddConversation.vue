<template>
  <div>
      <h1>Start a new Conversation</h1>
      <form @submit="addConvo">
      <input  v-model="text" type="text">
      <p>Author</p>
      <select  v-model="author" id="author">
        <option value="Alice">Alice</option>
        <option value="Bob">Bob</option>
      </select>
      <input type="submit">
      </form>
  </div>
</template>

<script>
export default {
    name: "AddConversation",
    props: ["author","text"],
    methods:{
         addConvo(e){
                e.preventDefault()
                const newConvo ={ 
                    author: this.author,
                    text: this.text
                }
            this.$emit('add-convo', newConvo)
            this.text=""
            this.author=""
            }
    }
}
</script>

<style>

</style>