<template>
  <main class="flex flex-col py-12 gap-8 bg-gray-900 items-center justify-center min-h-screen max-w-full w-full">
    <section class="w-full flex justify-center items-center">
      <h1 class="font-bold text-5xl md:text-7xl text-white">Poke<span class="text-red-600">Search</span></h1>
    </section>
    <section class="w-full flex justify-center items-center">
      <PokeBusca @queryPokemon="queryPokemon"></PokeBusca>
    </section>
  </main>
</template>

<script>
import PokeBusca from './components/PokeBusca.vue';

export default {
  name: "Main",
  components: {
    PokeBusca
  },
  data() {
    return {

    }
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
          console.log(this.evo_url);
        })
    },
  },
}
</script>