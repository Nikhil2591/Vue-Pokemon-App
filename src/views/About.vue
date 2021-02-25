<template>
  <div class="about">
    <div v-if="pokemon" class="w-3/12 m-auto bg-purple-100 mt-4 shadow-2xl flex justify-center flex-col items-center">
      <h3 class="text-2xl text-green-900 uppercase">{{ pokemon.name }}</h3>
      <div class="flex justify-center">
        <img className="w-60" :src="pokemon.sprites.front_shiny" alt="" />
        <img className="w-60" :src="pokemon.sprites.back_shiny" alt="" />
      </div>
      <div class="property">
        <h3 class="text-blue-400">Weight</h3>
        <div class="right">{{ pokemon.weight /10 }} kg</div>
      </div>
      <div class="property">
          <h3 class="text-green-400">Height</h3>
        <div class="right">{{ pokemon.height /10 }} m</div>
      </div>
      <h3 class="text-yellow-400"> Types</h3>
      <div v-for="(type, idx) in pokemon.types" :key="idx">
        <h5 class='text-blue-900'>{{ type.type.name }} </h5>
    </div>
  </div>
  </div>
</template>
<script>

import {useRoute} from "vue-router";
import {reactive, toRefs} from "vue";

export default {
  setup() {
  const route = useRoute();
    
  const state = reactive({
      pokemon: null
    });

    fetch(`https://pokeapi.co/api/v2/pokemon/${route.params.slug}/`)
    .then((res) => res.json())
    .then((data) =>{
      console.log(data);
      state.pokemon = data
    });

    return {... toRefs(state)}
  }
 
  
};
</script>