<template>
  <div>
      <h1>add a mutation</h1>
      <form @submit="addMutation">
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
    name: "addMutation",
    props: ["author","text"],
    methods:{
         addMutation(e){
                e.preventDefault()
                const newMutation ={ 
                    author: this.author,
                    text: this.text
                }
            this.$emit('add-mutation', newMutation)
            this.text=""
            this.author=""
            }
    }
}
</script>

<style>

</style>