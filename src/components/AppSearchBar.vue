<script>
import axios from 'axios';
export default {
  data() {
    return {
        // indirizzo API searchMovies
        apiAdress: 'https://api.themoviedb.org/3/search/movie',
        // Chiave API
        apiKey: 'a56a2d66f4601fa8078c3613712c7ef2',
        // Query per chiamate API
        apiQuery:"",
        // Creo una variabiale per tenere conto dell'input mandato dalla mia textBox
        inputSearch: ""
      
    }
  },
  methods:{
    // Metodo per effettuare una chiamata API per ricavare i vari film con le relative informazioni
    apiCall(apiKey, apiQuery){
        const apiUrl = `${this.apiAdress}?api_key=${this.apiKey}&query=${this.inputSearch}`
        axios.get(apiUrl)
        .then(function (response) {
            console.log(response);
          })
          .catch(function (error) {
            console.log(error);
          })
          .finally(function () {
            console.log('api calling..')
        });        
    }
  }
}
</script>

<template>
    <div class="input">
        <input type="text" id="txtSearch" v-model="inputSearch">
        <button id="btnSearch" class="btn btn-primary" @click="apiCall()">Search</button>

    </div>
</template>

<style lang="scss" scoped>
</style>