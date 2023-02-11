<template>
    <ul class="gap-8 grid grid-cols-1 lg:grid-cols-3">
        <PokeCard :pokemon="pokemon" v-for="pokemon in pokeProp" :key="pokemon.name">
        </PokeCard>
    </ul>
</template>
<script>

import PokeCard from './PokeCard.vue';
export default {

    components: {
        PokeCard,
    },

    props: {
        pokeProp: {
            type: Object,
            required: true
        },
    },
}
</script>
