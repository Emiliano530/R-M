<script>
import axios from 'axios'
let API_URL = `https://rickandmortyapi.com/api/character`
export default {
  data() {
    return {
      info: [],
      personajes: [],
      cont:1
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
    pagmas(num) {
      API_URL='https://rickandmortyapi.com/api/character/?page='+num
      console.log(API_URL)
      axios.get(API_URL)
      .then((response) => {
        console.log(response.config)
        this.info = response.data.info;
        this.personajes = response.data.results;
      })
      this.cont++
    },
    pagmenos(num) {
      API_URL='https://rickandmortyapi.com/api/character/?page='+num
      console.log(API_URL)
      axios.get(API_URL)
      .then((response) => {
        console.log(response.config)
        this.info = response.data.info;
        this.personajes = response.data.results;
      })
      this.cont--
    },
    buscador(text) {
      API_URL='https://rickandmortyapi.com/api/character/?name='+text ||'status='+text
      console.log(API_URL)
      axios.get(API_URL)
      .then((response) => {
        console.log(response.config)
        this.info = response.data.info;
        this.personajes = response.data.results;
      })
    }
  },
}
</script>

<template>

  //input y boton para buscador
  <input v-model="buscar" placeholder="Buscar" />
  <button @click="buscador(buscar)">Buscar</button>
  //

  //texto que muestra datos del api(ya estaba))
  <h2>Hay {{ info.count }} personajes en el programa de Rick & Morty</h2>

  //botones de anterior y siguiente(ya había pero lo edite)
  <button @click="pagmenos(cont)">Anterior</button>
  <a>{{ cont }}</a>
  <button @click="pagmas(cont)">Siguiente</button>
  <ul>
    <li v-for="p in personajes">
      <a>{{ p.name }} id:{{ p.id }}</a>
    </li>
  </ul>
</template>