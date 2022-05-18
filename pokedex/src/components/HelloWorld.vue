<script setup>
import { ref } from 'vue'
import axios from 'axios'

var name = ref("")

const pokemonInfos = () => axios.get('https://pokeapi.co/api/v2/pokemon/ditto')
  .then((response) => {
    // console.log(response.data)
  })
pokemonInfos()

const captureName = (formText) => {
  name = formText.data
  console.log("entrou?", formText)
}


console.log("name: ",name)
</script>

<template>
  <div>
    <input @input="captureName" placeholder="ENTER to search"  />
    <!-- <button v-on:click="captureName(pokemonName)">Search</button> -->
    <p>{{name}}</p>
  </div>
</template>

<style scoped>
a {
  color: #42b983;
}
</style>
