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
        this.txtSearch.focus();  
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
      const languages = {
        'en': '<span class="fi fi-gb"></span>', // Bandiera del Regno Unito
        'it': '<span class="fi fi-it"></span>', // Bandiera italiana
        'fr': '<span class="fi fi-fr"></span>', // Bandiera francese
        'de': '<span class="fi fi-de"></span>', // Bandiera tedesca
        'es': '<span class="fi fi-es"></span>', // Bandiera spagnola
        'ja': '<span class="fi fi-jp"></span>', // Bandiera giapponese
        'ko': '<span class="fi fi-kr"></span>', // Bandiera coreana
        'zh': '<span class="fi fi-cn"></span>', // Bandiera cinese
        'ru': '<span class="fi fi-ru"></span>', // Bandiera russa
        'pt': '<span class="fi fi-pt"></span>', // Bandiera portoghese
        'ar': '<span class="fi fi-ae"></span>', // Bandiera araba (Emirati Arabi Uniti)
        'hi': '<span class="fi fi-in"></span>', // Bandiera indiana
        'tr': '<span class="fi fi-tr"></span>', // Bandiera turca
        'nl': '<span class="fi fi-nl"></span>', // Bandiera olandese
        'sv': '<span class="fi fi-se"></span>', // Bandiera svedese
        'da': '<span class="fi fi-dk"></span>', // Bandiera danese
        'fi': '<span class="fi fi-fi"></span>', // Bandiera finlandese
        'th': '<span class="fi fi-th"></span>', // Bandiera tailandese
        'vi': '<span class="fi fi-vn"></span>', // Bandiera vietnamita
        'el': '<span class="fi fi-gr"></span>', // Bandiera greca
        'he': '<span class="fi fi-il"></span>', // Bandiera ebraica
      }
      return languages[lang] || 'Banidera non trovata!'
      },
      getIntVote(vote) {
       return Math.round(vote) / 2;
      }
    },
  
}
</script>

<template>
  <div class="nav">
    <div class="left">
      <h1 id="title-logo">BOOLFLIX</h1>
    </div>
    <div class="right">
      <div class="input">
        <input type="text" id="txtSearch" v-model="inputSearch" @keyup.enter="apiCall">
        <button id="btnSearch" class="btn btn-primary" @click="apiCall">Search</button>
      </div>
    </div>
  </div>
  
  
</template>

<style lang="scss" scoped>
.nav{
  padding: 10px 30px;
  height: 50px;
  background-color: black;
}

#title-logo{
  font-family: 'bebas neue', sans-serif;
  font-size: 40px;
  color: #E50914;
  letter-spacing: -2px;
  text-transform: uppercase;
}
</style>