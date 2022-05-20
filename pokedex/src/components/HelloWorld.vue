<script setup>
import { ref } from 'vue'
import axios from 'axios'

var completePokemonData = ref({})
const captureName = ref('')
var showHide = ref(false)
const image = ref({})
const icon = ref({})
const objectList = {name: '', sprite: ''}
var i = 1

while (i <= 898) {
  axios.get('https://pokeapi.co/api/v2/pokemon/'+i)
    .then((response) => {
      objectList.push({name: response.data.value.name, icon:'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-viii/icons/'+response.data.value.id+'.png'})
    })
    console.log(objectList)
    i++
}


const pokemonInfos = (props) => axios.get('https://pokeapi.co/api/v2/pokemon/'+props.toLowerCase())
  .then((response) => {
    completePokemonData.value = response.data
    console.log(completePokemonData.value)
    // image.value = completePokemonData.value.sprites.front_default
    // icon.value = 'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/versions/generation-viii/icons/'+completePokemonData.value.id+'.png'
    showHide.value = true
  })

</script>

<template>
  <div>
    <h1>POKÉDEX</h1>
    <div>
      <select>
        <option v-for="i in objectList">{{i.icon}} - {{i.name}}</option>
      </select>
    </div>
    <input v-model="captureName" @keydown.enter="pokemonInfos(captureName)" placeholder="ENTER to search"  />
    <!-- <button v-on:click="captureName(pokemonName)">Search</button> -->
    <!-- <p>{{completePokemonData.other.home.front_default}}</p> -->
    <div>
      <img v-if=showHide :src=icon />
      <img v-if=showHide :src=image />
    </div>
  </div>
</template>

<style scoped>
a {
  color: #42b983;
}
</style>
