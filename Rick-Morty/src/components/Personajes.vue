<script>
import axios from "axios";
let API_URL = `https://rickandmortyapi.com/api/character`;
export default {
  data() {
    return {
      info: [],
      personajes: [],
      pagina: 1,
      siguiente: null,
      anterior: null,
      buscar: "",
    };
  },
  mounted() {
    axios.get(API_URL).then((response) => {
      this.info = response.data.info;
      this.personajes = response.data.results;
    });
  },

  methods: {
    navpag(num) {
      API_URL =
        "https://rickandmortyapi.com/api/character/?page=" + this.pagina;
      console.log(API_URL);
      axios.get(API_URL).then((response) => {
        console.log(response.config);
        this.info = response.data.info;
        this.personajes = response.data.results;
      });
    },
    buscador(text) {
      API_URL =
        "https://rickandmortyapi.com/api/character/?" +
        ("name=" + text || "&status=" + text);
      console.log(API_URL);
      axios.get(API_URL).then((response) => {
        console.log(response.config);
        this.info = response.data.info;
        this.personajes = response.data.results;
      });
    },
    mostrar() {
      open="../components/datos.vue";
    },
  },
};
</script>

<template>
  <div class="text-center">
    <div>
      <div class="flex justify-center gap-6 p-5 pb-5">
        <input v-model="buscar" placeholder="Buscar" />
        <button class="button bg-white text-black" @click="buscador(buscar)">Buscar</button>
      </div>

      <h2>Hay {{ info.count }} personajes en el programa de Rick & Morty</h2>
      <div class="flex justify-center gap-6 p-5 pb-0">
        <button
          class="button bg-white text-black w-20"
          v-if="pagina !== 1"
          @click="navpag(pagina--)"
        >
          Anterior
        </button>
        <a>{{ pagina }}</a>
        <button
          class="button bg-red-700 w-20"
          v-if="pagina !== this.info.pages"
          @click="navpag(pagina++)"
        >
          Siguiente
        </button>
      </div>
    </div>
    <div>
      <ul class="grid grid-cols-4">
        <li
          class="card bg-black rounded-3xl m-5 scale-75 cursor-pointer hover:rotate-2" v-on:click="mostrar()"
          v-for="p in personajes"
        >
          <img
            class="rounded-t-3xl"
            v-bind:src="p.image"
            alt="Imagen_Personaje"
          />
          <a>{{ p.name }}</a>
        </li>
      </ul>
    </div>
    <div class="flex justify-center gap-6 p-5 pb-0">
        <button
          class="button bg-white text-black w-20"
          v-if="pagina !== 1"
          @click="navpag(pagina--)"
        >
          Anterior
        </button>
        <a>{{ pagina }}</a>
        <button
          class="button bg-red-700 w-20"
          v-if="pagina !== this.info.pages"
          @click="navpag(pagina++)"
        >
          Siguiente
        </button>
      </div>
  </div>
</template>
