<template>
    <div class="relative group w-10/12 md:w-7/12 lg:w-5/12">
        <input v-model="query" placeholder="Digite um nome de Pokemon aqui!"
            class="bg-transparent pl-4 w-full hover:bg-gray-800 text-white placeholder:text-white/20 font-normal focus:border-0 focus:bg-gray-800 focus:outline-0 duration-300 hover:duration-300 ease-in-out shadow-gray-900 hover:border-gray-900 rounded-full border border-white/30 py-3">
        <button @click="buscarPokemon" class="absolute inset-y-0 r right-0 flex items-center pr-4 ">
            <MagnifyingGlassIcon class="w-5 group-hover:text-white duration-300  h-5 text-white/30" />
        </button>
    </div>
</template>