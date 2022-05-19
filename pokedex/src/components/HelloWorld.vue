<script setup>
import { ref } from 'vue'
import axios from 'axios'

var completePokemonData = ref({})
const captureName = ref('')
var showHide = ref(false)
const image = ref({})

const pokemonInfos = (props) => axios.get('https://pokeapi.co/api/v2/pokemon/'+props.toLowerCase())
  .then((response) => {
    completePokemonData.value = response.data
    image.value = completePokemonData.value.sprites.other.home.front_default
    showHide.value = true
  })

</script>

<template>
  <div>
    <h1>POKÉDEX</h1>
    <input v-model="captureName" @keydown.enter="pokemonInfos(captureName)" placeholder="ENTER to search"  />
    <!-- <button v-on:click="captureName(pokemonName)">Search</button> -->
    <!-- <p>{{completePokemonData.other.home.front_default}}</p> -->
    <div>
      <img v-if=showHide :src=image />
    </div>
  </div>
</template>

<style scoped>
a {
  color: #42b983;
}
</style>
