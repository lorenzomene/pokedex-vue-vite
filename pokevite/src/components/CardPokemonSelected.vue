<script setup>
const pokemon = defineProps({
    name: {
        type: String
    },
    xp: {
        type: Number
    },
    height: {
        type: Number
    },
    img:{
        type: String
    },
    loading: {
        type: Boolean
    }
})
</script>

<template>
        <div class="card cardPokemonSelected" 
        :class="loading ? '' : 'animate__animated animate__flipInY'">
            <img v-if="pokemon.name" :src="pokemon.img" class="card-img-top" 
            :alt="pokemon.name">
            <img v-else src="../assets/egg_pokemon.svg" class="card-img-top" 
            alt="???">
            <div class="card-body">
              <h5 class="card-title text-center">{{ pokemon.name || '???' }}</h5><hr>
              <div class="row">
                <section class="col">
                    <strong>XP:</strong>
                    <span>{{ pokemon.xp }}</span>
                </section>
                <section class="col">
                    <strong>Height:</strong>
                    <span>{{pokemon.height}}</span>
                </section>
              </div>
            </div>
        </div>
</template>

<style scoped>
.cardPokemonSelected{
    background: rgb(63,94,251);
    background: radial-gradient(circle, rgba(63,94,251,1) 0%, rgba(252,70,107,1) 100%);
    height: 75vh;
}
.cardPokemonSelected img{
    height: 250px;
}

@media (max-width: 768px) {
    .cardPokemonSelected{
        height: 30vh;
        width: 50%;
        margin: 0 auto 10px auto;
    }
    .cardPokemonSelected img{
        height: 120px;
    }
}
    
</style>