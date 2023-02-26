<script>
import axios from 'axios'
let API_URL = `https://rickandmortyapi.com/api/character`
export default {
  data() {
    return {
      info: [],
      personajes: [],
      pagina:1,
      siguiente:null,
      anterior:null,
      buscar:'',
    }
  },
  mounted() {
    axios.get(API_URL)
      .then((response) => {
        this.info = response.data.info;
        this.personajes = response.data.results;
      })
  },
  
  methods: {
    navpag(num) {
      API_URL='https://rickandmortyapi.com/api/character/?page='+num
      console.log(API_URL)
      axios.get(API_URL)
      .then((response) => {
        console.log(response.config)
        this.info = response.data.info;
        this.personajes = response.data.results;
      })
    },
    buscador(text) {
      API_URL='https://rickandmortyapi.com/api/character/?'+('name='+text ||'&status='+text)
      console.log(API_URL)
      axios.get(API_URL)
      .then((response) => {
        console.log(response.config)
        this.info = response.data.info;
        this.personajes = response.data.results;
      })
    },
  },
}

</script>

<template >
  <div class="text-center">
    <input v-model="buscar" placeholder="Buscar" />
  <button @click="buscador(buscar)">Buscar</button>

  <h2>Hay {{ info.count }} personajes en el programa de Rick & Morty</h2>

  <button class="button bg-white text-black" v-if="pagina!==1" @click="navpag(pagina--)">Anterior</button>
  <a>{{pagina }}</a>
  <button class="button bg-red-700" v-if="pagina!==this.info.pages+1" @click="navpag(pagina++)">Siguiente</button>
  <ul>
    <li v-for="p in personajes">
      <a>{{ p.name }}</a>
      <img class="rounded-3xl scale-50" v-bind:src=" p.image " alt="Imagen_Personaje">
    </li>
  </ul>
  </div>
</template>