<template>
  <main class="flex flex-col py-12 gap-8 bg-gray-900 items-center justify-center min-h-screen max-w-full w-full">
    <section class="w-full flex justify-center items-center">
      <h1 class="font-bold text-5xl md:text-7xl text-white">Poke<span class="text-red-600">Search</span></h1>
    </section>
    <section class="w-full flex gap-12 flex-col justify-center items-center">
      <PokeBusca @queryPokemon="queryPokemon"></PokeBusca>
      <PokeLista :pokeProp="pokemonData"></PokeLista>
    </section>
  </main>
</template>

<script>
import PokeBusca from './components/PokeBusca.vue';
import PokeLista from './components/PokeLista.vue';
import PokeError from './components/PokeError.vue';

export default {
  name: "Main",
  components: {
    PokeBusca, PokeLista, PokeError
  },
  data() {
    return {
      evo_url: {},
      evolucoes: [],
      pokemonData: [],
      error: false,
      speciesData: [],
    };
  },
  methods: {
    async queryPokemon(query) {
      fetch(`https://pokeapi.co/api/v2/pokemon-species/${query}`)
        .then((res) => {
          if (res.ok) {
            this.error = false;
            return res.json();
          } else {
            this.error = true;
            console.log(this.error);
          }
        })
        .then((data) => {
          this.evo_url = data.evolution_chain.url
          this.buscarEvos();
          this.speciesData = data;
        })
    },
    buscarEvos() {
      fetch(this.evo_url).then((res) => res.json())
        .then((data) => {
          this.evolucoes = data;
          this.parseChain();
        })
    },
    async parseChain() {
      this.pokemonData = [];
      let evoData = this.evolucoes.chain;
      do {
        let speciesName = evoData.species.name;
        fetch(`https://pokeapi.co/api/v2/pokemon/${speciesName}`).then((res) => res.json())
          .then((data) => {
            this.pokemonData.push({
              "name": data.name,
              "sprites": data.sprites,
              "color": this.speciesData.color,
              "stats": data.stats
            });
          })
        evoData = evoData['evolves_to'][0];
      } while (!!evoData && evoData.hasOwnProperty('evolves_to'));
    },
  },
}
</script>