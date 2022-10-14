<template>
  <div class="container">
    <img alt="Vue logo" src="./assets/logo.png"/>
    <h1 class="title is-3">Rick & Morty API</h1>
    <input
      class="input is-normal"
      type="text"
      placeholder="Pesquise pelo nome do personagem"
      v-model="this.searchQuerie"
    />
    <button id="searchButton" class="button is-primary is-fullwidth" @click="searchResource">Buscar</button>
    <hr/>
    <div v-for="item in filtrededSearch" :key="item.name">
      <MainComponent :name="item.name" :gender="item.gender" :image="item.image"/>
    </div>
  </div>
</template>

<script>
import MainComponent from "./components/MainComponent";
import axios from "axios"

export default {
  name: "App",
  components: {
    MainComponent,
  },
  data() {
    return {
      items : [],
      searchQuerie : "",
      filtrededSearch: []
    }
  },
  created() {
    axios.get("https://rickandmortyapi.com/api/character").then((res) => {
      res.data.results.forEach((element) => {
          this.items.push({
            name: element.name,
            image: element.image,
            gender: element.gender
          });
      });
      this.filtrededSearch = this.items
    }).catch((err) => {
      console.log(err)
    })
  },
  methods: {
    searchResource: function() {
      this.filtrededSearch = []
      if(this.searchQuerie === "" || this.searchQuerie === " " || this.searchQuerie === undefined){
        this.filtrededSearch = this.items
      } else {
        this.items.forEach((arr) => {
          if(arr.name.toLowerCase().trim().startsWith(this.searchQuerie.toLowerCase().trim())) {
            this.filtrededSearch.push(arr)
          }
        })
      }
    }
  },
  /* computed: {
    filterResources() {
      if(this.searchQuerie === "" || this.searchQuerie === " " || this.searchQuerie === undefined) {
        return this.items
      } else {
        return this.items.filter(item => item.name.toLowerCase().startsWith(this.searchQuerie.toLowerCase()))
      }
    }
  } */
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#searchButton {
  margin: 1% 0;
}
</style>
