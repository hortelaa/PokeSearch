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
            <table class="table-auto text-white">
                <thead :style="{ color: pokemon.color.name }">
                    <th>Stats</th>
                    <th>Valor</th>
                </thead>
                <tbody>
                    <tr class=" w-full border-b-[0.075rem] border-white/30" v-for="stat in pokemon.stats"
                        :key="stat.stat.name">
                        <td class=" first-letter:uppercase font-bold py-2">{{ stat.stat.name }}</td>
                        <td class=" first-letter:uppercase px-4 py-2">{{ stat.base_stat }}</td>
                    </tr>
                    <h2 :style="{ color: pokemon.color.name }" class="font-bold py-2">Tipo</h2>
                    <tr class="flex pb-2 gap-4" v-for="type in pokemon.types" :key="type.type.name">
                        <td class="bg-gray-500 p-1 first-letter:uppercase font-bold rounded-xl ">{{
                            type.type.name
                        }}
                        </td>
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
}
</script>