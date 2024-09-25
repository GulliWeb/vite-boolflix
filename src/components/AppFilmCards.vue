<script>
export default {
  props: {
    films: {
      type: Array,
      required: true
    },
    tvSeries: {
      type: Array,
      required: true,
    }
  }, 
  data() {
    return {
      
    }
  },
  methods:{
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
      },
  }
}
</script>

<template>
  <!-- Lista Film -->
  <div class="card-wrapper d-flex">
    <ul>
      <li id="card" v-for="film in films" :key="film.id" class="card">
        <img :src="`https://image.tmdb.org/t/p/w342${film.poster_path}`" alt="Poster">
        <div class="overlay">
          <h2>{{ film.title }}</h2>
          <p><span id="original-title">Original title:</span> {{ film.original_title }}</p>
          <p><span class="vote">Vote: </span>{{ getIntVote(film.vote_average) }}</p>
          <p v-if="film.overview">{{ film.overview }}</p>
        </div>
        <p v-html="setFlag(film.original_language)"></p>
        <div>
          <span v-if="getIntVote(film.vote_average) === 0">
            Votazione non disponibile
          </span>
          <!-- Ciclo per stampare le stelle per i film -->
          <i v-else v-for="n in 5" :key="n" class="fa-star" :class="(n <= getIntVote(film.vote_average)) ? 'fas' : 'far'"></i>
        </div>
      </li>
    </ul>

    <!-- Lista Serie TV -->
    <ul>
      <li id="card" v-for="serie in tvSeries" :key="serie.id" class="card">
        <img :src="`https://image.tmdb.org/t/p/w342${serie.poster_path}`" alt="Poster">
        <div class="overlay">
          <h2>{{ serie.name }}</h2>
          <p>Original name: {{ serie.original_name }}</p>
          <p><span class="vote">Vote: </span>{{ getIntVote(serie.vote_average) }}</p>
          <p v-if="serie.overview">{{ serie.overview }}</p>
        </div>
        <p v-html="setFlag(serie.original_language)"></p>
        <div>
          <!-- Ciclo per stampare le stelle per le serie TV -->
          <i v-for="n in 5" :key="n" class="fa-star" :class="(n <= getIntVote(serie.vote_average)) ? 'fas' : 'far'"></i>
        </div>
      </li>
    </ul>
  </div>
</template>

<style lang="scss" scoped>
body{
  background-color: rgb(20, 20, 20);
}

.card-wrapper {
  display: flex;
  flex-wrap: wrap;
  justify-content: center; 
  margin: 20px;
}

ul {
  list-style-type: none; 
  padding: 0; 
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around; 
  width: 100%; 
}

li {
  background: #fff;
  border-radius: 10px; 
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1); 
  margin: 15px; 
  width: 300px; 
  transition: transform 0.3s, border-radius 0.3s; 
  overflow: hidden; 
  text-align: center; 
}

li:hover {
  border-radius: 10px;

}

img {
  width: 100%; 
  border-bottom: 4px solid #f0c14b;
}

h2 {
  font-size: 1.5rem; 
  color: #333; 
  margin: 10px 0;
}

p {
  color: #666; 
  margin: 5px 0; 
}

.fa-star {
  color: #f0c14b; 
}

// EFFETTO OVERLAY SU HOVER CARD
.card {
  position: relative; 
  background: #fff;
  border-radius: 10px; 
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1); 
  margin: 15px; 
  width: 300px; 
  transition: transform 0.3s, border-radius 0.3s; 
  overflow: hidden; 
  text-align: center; 
}

.card:hover {
  transform: scale(1.05); 
}

.overlay {
  padding: 15px; 
  position: absolute; 
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.85); 
  color: white;
  display: flex;
  flex-direction: column;
  justify-content: center; 
  align-items: center; 
  opacity: 0; 
  transition: opacity 0.3s ease, transform 0.3s ease; 
  backdrop-filter: blur(5px);
  overflow: auto
}

.text-container {
  max-height: 100px; 
  overflow: auto; 
  text-align: center; 
}

.card:hover .overlay {
  opacity: 1; 
  transform: scale(1.05); 
}

h2 {
  font-size: 1.8rem; 
  margin: 10px 0;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.5); 
}

p {
  color: #ddd; 
  margin: 5px 0; 
  font-weight: bold;
}

#original-title {
  font-weight: normal;
  color: #fff; 
}

.vote {
  font-weight: normal;
  color: #f0c14b; 
}

.fa-star {
  color: #f0c14b; 
}
</style> 