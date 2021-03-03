<template>
<div>
<h2>{{pokemonDetail.name}}</h2>
<h2>{{pokemonDetail.id}}</h2>
</div>

</template>

<script>
import axios from 'axios'
export default {
  name: "DetailPokemon",
  data() {
    return {
      pokemonURL: this.$route.params.pokemon,
      pokemonDetail: []
    };
  },
  created: async function () {
    try {
      const res = await axios.get(
      this.$route.params.pokemon
      );
      this.pokemonDetail = res.data;
      console.log(res.data);
    } catch (error) {
      console.log(error);
    }
  },
};
</script>

<style>
</style>