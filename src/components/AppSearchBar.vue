<script>
import axios from 'axios';
import AppFilmCards from './AppFilmCards.vue';
export default {
  components:{
    AppFilmCards
  },
  data() {
    return {
      // Array di oggetti film che verrà popolato dalla chiamata API
      films: [],
      tvSeries: [],
      title: [],
      originalTitle: [],
      lang: [],
      vote: [],
      // indirizzo API searchMovies
      apiFilmAddress: 'https://api.themoviedb.org/3/search/movie',
      apiTvSeriesAddress: 'https://api.themoviedb.org/3/search/tv',
      // Chiave API
      apiKey: 'a56a2d66f4601fa8078c3613712c7ef2',
      // Variabile per l'input mandato dalla textBox
      inputSearch: "",
      isSearchVisible: false,
    };
  },
  methods: {
    // Metodo per effettuare una chiamata API per ricavare i vari film con le relative informazioni
    apiCall() {
      // Controllo che verifica se l'input è vuota
      
      const apiUrl = `${this.apiFilmAddress}?api_key=${this.apiKey}&query=${this.inputSearch}`;
      const apiTvSeriesUrl = `${this.apiTvSeriesAddress}?api_key=${this.apiKey}&query=${this.inputSearch}`;
      // Chiamata tramite Axios film
      axios.get(apiUrl)
        .then((response) => {
          console.log(response.data.results);
          this.films = response.data.results;
        })
        .catch(function (error) {
          console.log(error);
        })
        .finally(function () {
          console.log('api calling..');
        });

        // Chiamata tramite Axios serie tv
        axios.get(apiTvSeriesUrl)
        .then((response) => {
          console.log(response.data.results);
          this.tvSeries = response.data.results;
        })
        .catch(function (error) {
          console.log(error);
        })
        .finally(function () {
          console.log('api tv series calling..');
        });
    },
      // Metodo per mostrare barra di ricerca
      toggleSearch(){
       this.isSearchVisible = true
      }
    },
}
</script>

<template>
  <div class="nav d-flex">
    <div class="left d-flex align-items-center">
      <h1 id="title-logo" class="mb-0">BOOLFLIX</h1>
      <ul class="d-flex mb-0">
        <li><a href="#">Home</a></li>
        <li><a href="#tvSeries">Serie tv</a></li>
        <li><a href="#film">Film</a></li>
      </ul>
    </div>
    <div class="right d-flex align-items-center justify-content-end">
      <div class="input d-flex align-items-center">
        <input v-if="isSearchVisible" type="text" placeholder="Titoli, Serie tv.." id="txtSearch" v-model="inputSearch" @keyup.enter="apiCall">
        <i id="btnSearch" class="fas fa-search" @click="apiCall" @mouseenter=" toggleSearch" ></i>
        <figure id="profile-avatar">
          <img src="../assets/img/netflix-profile-pictures-1000-x-1000-2fg93funipvqfs9i.jpg" alt="">
        </figure>
      </div>
    </div>
  </div>
  
  <!-- COLLEGAMENTO TRAMITE PROPS AL COMPONENTE FILM CARDS -->
   <AppFilmCards :films="films" :tvSeries="tvSeries"/>
  
</template>

<style lang="scss" scoped>
body{
  font-family: 'Roboto';
}

.nav{
  position: sticky;
  top: 0;
  z-index: 2;
  width: 100%;
  height: 50px;
  background-color: black;
}

// LEFT
.left, .right{
  padding-left:30px;
}

ul li{
  list-style-type: none;
}

ul li a {
  font-size: 14px;
  text-decoration: none;
  color: #fff;
  margin-right: 25px;
}

ul li a:hover{
  color: lightgray;
  cursor: pointer;
}

ul li a:active{
  color: #fff;
}

#title-logo{
  font-family: 'bebas neue', sans-serif;
  font-size: 40px;
  color: #E50914;
  letter-spacing: -2px;
  text-transform: uppercase;
  transition: transform 0.3s ease;
}

#title-logo:hover{
  transform: scale(1.1) rotate(5deg);
  text-shadow: 0 0 10px rgba(255, 255, 255, 0.7); 
  cursor: crosshair;
}
// RIGHT
.right{
  flex-grow: 1;
  padding-right: 30px;
}

.right i{
  font-size: 25px;
  color: #fff;
  margin-left: 10px;
  margin-right: 10px;
}

.right i:hover{
  cursor: pointer;
  color: lightgray;
}

.right i:active{
  color: #fff;
}

#profile-avatar{
  margin-bottom: 0;
  max-width: 35px;
}

img{
  max-width: 100%;
  border-radius: 5px;
  transition: transform 0.3s ease;
}

img:hover{
  transform: scale(1.1)
}

img:active {
  transform: scale(0.95);
}

input{
  border-radius: 5px;
  padding-left: 10px;
  border: 1px solid white
}
</style>