<template>
<div>
  <img :src="picture" length="100" width="100">
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
      pokemonDetail: [],
      picture: ''
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
    try {
      var id = this.$route.params.pokemon.split('/');
      this.picture = `https://pokeres.bastionbot.org/images/pokemon/${id[id.length-2]}.png`

    } catch (error) {
      console.log(error);
    }
  },
};
</script>

<style>
</style>