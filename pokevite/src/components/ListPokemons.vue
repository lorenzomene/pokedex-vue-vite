<script setup>
const pokemon = defineProps({
    name: {
        type: String
    },
    urlBaseSvg: {
        type: String
    }
})

</script>

<template>
  <div class="col-4 col-md-6 col-lg-4">
    <div class="card p-2 mb-3 cardListPokemon" style="height: 160px;"> 
        <p class="text-center">{{ pokemon.name }}</p> 
        <img :src="urlBaseSvg" class="card-img-top" 
        alt="..."
        height="80">   
    </div>
  </div>
</template>

<style scoped>
.cardListPokemon{
    background: rgb(63,94,251);
    background: radial-gradient(circle, rgba(63,94,251,1) 0%, rgba(252,70,107,1) 100%);
    cursor: pointer;
}
.cardListPokemon:hover{
    background: rgb(252,70,107);
    background: radial-gradient(circle, rgba(252,70,107,1) 0%, rgba(63,94,251,1) 100%);
}
.cardListPokemon img:hover{
    padding: .1rem;
}
</style>