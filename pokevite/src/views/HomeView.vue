<script setup>
import { onMounted, reactive, ref, computed } from 'vue'
import ListPokemons from "../components/ListPokemons.vue" 
import CardPokemonSelected from "../components/CardPokemonSelected.vue" 

let urlBaseSvg = ref("https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/") //dream-world
let pokemons = reactive(ref());
let searchPokemonField = ref("");
let pokemonSelected = reactive(ref());
let loading = ref(false);

onMounted(() => {
  fetch("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
  .then(res => res.json())
  .then(res => {
    pokemons.value = res.results
  })
})

const pokemonsFiltered = computed(() => {
  if(pokemons.value && searchPokemonField.value){
    return pokemons.value.filter(pokemon => {
      return pokemon.name.toLowerCase().includes(searchPokemonField.value.toLowerCase())
    })
  }
  return pokemons.value
})

const selectPokemon = async (pokemon) => {
  loading.value = true;
  await fetch(pokemon.url)
  .then(res => res.json())
  .then(res => {
    pokemonSelected.value = res
  })
  .catch(err => {
    alert(err)
  })
  .finally(() => {
    loading.value = false;
  })
}

</script>

<template>
  <main>
    <div class="container text-center">
      <div class="row mt-4">

        <div class="col-sm-12 col-md-6">
          <CardPokemonSelected 
          :name="pokemonSelected?.name"
          :xp="pokemonSelected?.base_experience"
          :height="pokemonSelected?.height"
          :img="pokemonSelected?.sprites.other.dream_world.front_default"
          :loading="loading"
          />
        </div>

        <div class="col-sm-12 col-md-6">
          <div class="card card-list">
            <div class="card-body row">

              <div class="mb-3">
                <label hidden for="searchPokemonField" class="form-label">Search...</label>
                <input type="text" class="form-control" id="searchPokemonField" 
                placeholder="Search..." v-model="searchPokemonField">
              </div>

              <ListPokemons 
              v-for="pokemon in pokemonsFiltered"
              :key="pokemon.name"
              :name="pokemon.name"
              :urlBaseSvg="urlBaseSvg + pokemon.url.split('/')[6] + '.svg'"
              @click="selectPokemon(pokemon)"
              />
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
.card-list{
  overflow-y: scroll;
  overflow-x: hidden;
  max-height: 75vh;
}
</style>