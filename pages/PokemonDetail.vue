<template>
<div>
 
<h2>{{pokemonDetail.id}} {{pokemonDetail.name}}</h2>
 <img :src="picture" length="100" width="100"><br>
<table>
<td>
  <tr>Abilities:</tr>
</td>
<td>
<tr  v-for="abilities in pokemonDetail.abilities" v-bind:key="abilities.name">
  {{abilities.ability.name}} 
</tr>
</td>
</table>

<table>
<td>
  <tr>Type:</tr>
</td>
<td>
<tr  v-for="types in pokemonDetail.types" v-bind:key="types.name">
  {{types.type.name}} 
</tr>
</td>
</table>
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