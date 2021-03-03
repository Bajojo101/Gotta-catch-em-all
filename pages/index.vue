<template>
  <div>
   <button
      class="grid-icon"
      v-bind:class="{ active: layout == 'grid' }"
      v-on:click="layout = 'grid'"
    >
      Grid View
    </button>
    <button
      class="list-icon"
      v-bind:class="{ active: layout == 'list' }"
      v-on:click="layout = 'list'"
    >
      List View
    </button>

    <ul v-if="layout === 'list'" class="list">
      <li v-for="pokemon in pokemons" v-bind:key="pokemon.name">
        <p>{{ pokemon.name }}</p>
      </li>
    </ul>

    <ul v-if="layout === 'grid'" class="grid">
      <li v-for="pokemon in pokemons" v-bind:key="pokemon.name"></li>
      <p>Hallo</p>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
import Grid from "vue-virtual-scroll-grid";
export default {
  name: "App",
  components: {
    Grid,
  },
  data() {
    return {
      pokemons: [],
      layout: "list",
    };
  },
  created: async function () {
    try {
      const res = await axios.get(
        "https://pokeapi.co/api/v2/pokemon?limit=151"
      );
      this.pokemons = res.data.results;
      console.log(res);
    } catch (error) {
      console.log(error);
    }
  },
  methods: {

  },
};
</script>

<style>

</style>
