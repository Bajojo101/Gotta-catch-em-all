<template>
  <div>
    <button
      class="button"
      v-bind:class="{ active: layout == 'grid' }"
      v-on:click="layout = 'grid'"
    >
      Grid View
    </button>
    <button
      class="button"
      v-bind:class="{ active: layout == 'list' }"
      v-on:click="layout = 'list'"
    >
      List View
    </button>

    <ul v-if="layout === 'list'" class="list">
      <li v-for="(pokemon, index) in pokemons" v-bind:key="pokemon.name">
        <nuxt-link
          :to="{ name: 'PokemonDetail', params: { pokemon: pokemon.url } }"
        >
        {{index+1}}
        {{ pokemon.name }}
        </nuxt-link>
      </li>
    </ul>
    <div v-if="layout === 'grid'" class="grid-container">
      <div v-for="(pokemon, index) in pokemons" v-bind:key="pokemon.name">
        <nuxt-link
          :to="{ name: 'PokemonDetail', params: { pokemon: pokemon.url } }"
        >
          {{index +1}}
          {{ pokemon.name }}
        </nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "App",
  components: {},
  data() {
    return {
      pokemons: [],
      layout: "grid",
    };
  },
  created: async function () {
    try {
      const res = await axios.get(
        "https://pokeapi.co/api/v2/pokemon?limit=151"
      );
      this.pokemons = res.data.results;
    } catch (error) {
      console.log(error);
    }
  },
  methods: {},
};
</script>

<style>
* {
  box-sizing: border-box;
  font-family: Arial, Helvetica, sans-serif;
  
}

.button {
  background-color: #2196f3;
  border: none;
  color: white;
  padding: 15px 32px;
  margin-bottom: 10px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
}

/* Grid layout */
.grid-container {
  display: grid;
  grid-template-columns: auto auto auto;
  grid-gap: 10px;
  background-color: #2196f3;
  padding: 10px;
}

.grid-container > div {
  background-color: rgba(255, 255, 255, 0.8);
  text-align: center;
  padding: 20px 0;
  font-size: 20px;
}
.grid-container div:hover {
  background-color: #fff;
}
.grid-container div:hover a {
  color: #0096d4;
}

.grid-container div a {
  color: #000;
  display: table-cell;
  font-weight: 700;
  padding: 0 0 0 15px;
  vertical-align: middle;
  width: 100%;
  text-decoration: none;
}

/* List layout */
.list {
  background-color: #ddedfb;
  font-size: 20px;
  list-style: none;
  margin: 0 auto;
  padding: 0;
  text-align: left;
  width: 100%;
}

.list li {
  border-bottom: 1px solid #fff;
  overflow: hidden;
  padding: 20px;
}

.list li:hover {
  background-color: #fff;
}

.list li:hover a {
  color: #0096d4;
}

.list li a {
  color: #000;
  display: table-cell;
  font-weight: 700;
  padding: 0 0 0 15px;
  vertical-align: middle;
  width: 100%;
  text-decoration: none;
}
</style>
