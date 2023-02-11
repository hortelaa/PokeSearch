<template>
    <li :style="{ borderColor: pokemon.color.name }"
        class="flex bg-gray-800 cursor-pointer border-t-2 w-80 p-4 items-center shadow-gray-800 rounded-lg flex-col gap-4">
        <div @click="showCardFront = !showCardFront" :class="{ 'flex': showCardFront, 'hidden': !showCardFront }"
            class="flex items-center flex-col justify-center">
            <h2 class="text-lg font-bold first-letter:uppercase text-white">
                {{ pokemon.name }}
            </h2>
            <figure>
                <img :src="pokemon.sprites.other.home.front_default" :alt="pokemon.name">
            </figure>
        </div>
        <div class="py-4" @click="showCardFront = !showCardFront" v-if="!showCardFront">
            <table class=" text-white">
                <thead>
                    <tr>
                        <th class="px-4 py-2">Stats</th>
                        <th class="px-4 py-2">Valor</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="stat in pokemon.stats" :key="stat.stat.name">
                        <td class="border px-4 py-2">{{ stat.stat.name }}</td>
                        <td class="border px-4 py-2">{{ stat.base_stat }}</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </li>
</template>


<script>
export default {
    props: {
        pokemon: {
            type: Object,
        },
    },
    data() {
        return {
            color: this.pokemon.color,
            showCardFront: true,
        }
    },
    created() {
        console.log(this.pokemon.stats);
    }
}
</script>