<script>
import axios from 'axios';
export default {
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
      inputSearch: ""
    };
  },
  methods: {
    // Metodo per effettuare una chiamata API per ricavare i vari film con le relative informazioni
    apiCall() {
      // Controllo che verifica se l'input è vuota
      if (!this.inputSearch) {
        alert('Attenzione! campo di ricerca vuoto.');
        this.$refs.txtSearch.focus();  // Usando ref per focalizzare l'input
        return;
      }
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
    // Metodo per visualizzare in pagina la bandiera corrispondente alla lingua del film e serie tv
    setFlag(lang) {
  switch (lang) {
      case 'en':
        return 'INGLESE!';
      case 'it':
        return 'ITALIANO!';
      case 'fr':
        return 'FRANCESE!';
      case 'de':
        return 'TEDESCO!';
      case 'es':
        return 'SPAGNOLO!';
      case 'ja':
        return 'GIAPPONESE!';
      case 'ko':
        return 'COREANO!';
      case 'zh':
        return 'CINESE!';
      case 'ru':
        return 'RUSSO!';
      case 'pt':
        return 'PORTOGHESE!';
      case 'ar':
        return 'ARABO!';
      case 'hi':
        return 'HINDI!';
      case 'tr':
        return 'TURCO!';
      default:
        return 'Lingua non riconosciuta';
    }
   },
   getIntVote(vote) {
   const starCount = Math.round(vote) / 2;
   const stars = []

   for (let i = 0; i < starCount.length; i++) {
    stars.push(i + 1)
   }
   return stars
   }
},
  
}
</script>

<template>
  <div class="input">
    <input type="text" id="txtSearch" v-model="inputSearch" @keyup.enter="apiCall">
    <button id="btnSearch" class="btn btn-primary" @click="apiCall">Search</button>
  </div>

  <!-- Lista Film -->
  <ul>
    <li v-for="film in films" :key="film.id">
      <img :src="`https://image.tmdb.org/t/p/w342${film.poster_path}`" alt="Poster">
      <h2>{{ film.title }}</h2>
      <p>{{ film.original_title }}</p>
      <p>{{ film.original_language }} - {{ setFlag(film.original_language) }}</p> 
      <p>{{ film.vote_average }}</p> 
      <div>
        <!-- Ciclo per stampare le stelle per i film -->
        <i v-for="n in getIntVote(film.vote_average)" :key="n" class="fas fa-star"></i>
      </div>
    </li>
  </ul>

  <!-- Lista Serie TV -->
  <ul>
    <li v-for="serie in tvSeries" :key="serie.id">
      <img :src="`https://image.tmdb.org/t/p/w342${serie.poster_path}`" alt="Poster">
      <h2>{{ serie.name }}</h2>
      <p>{{ serie.original_name }}</p>
      <p>{{ setFlag(serie.original_language) }}</p> 
      <p>{{ getIntVote(serie.vote_average) }}</p> 
      <div>
        <!-- Ciclo per stampare le stelle per le serie TV -->
        <i v-for="n in getIntVote(serie.vote_average)" :key="n" class="fas fa-star"></i>
      </div>
    </li>
  </ul>
</template>

<style lang="scss" scoped>
</style>