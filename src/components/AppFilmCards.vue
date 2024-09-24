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
  <ul>
    <li v-for="film in films" :key="film.id">
      <img :src="`https://image.tmdb.org/t/p/w342${film.poster_path}`" alt="Poster">
      <h2>{{ film.title }}</h2>
      <p>{{ film.original_title }}</p>
      <p v-html="setFlag(film.original_language)"></p>
      <div>
        <span v-if="getIntVote(film.vote_average) === 0">
          Votazione non disponibile
        </span>
        <!-- Ciclo per stampare le stelle per i film -->
        <i v-else v-for="n in 5" :key="n" class="fa-star" :class="(n <= getIntVote(film.vote_average)) ? 'fas' : 'far' "></i>
      </div>
    </li>
  </ul>
   
  <!-- Lista Serie TV -->
  <ul>
    <li v-for="serie in tvSeries" :key="serie.id">
      <img :src="`https://image.tmdb.org/t/p/w342${serie.poster_path}`" alt="Poster">
      <h2>{{ serie.name }}</h2>
      <p>{{ serie.original_name }}</p>
      <p v-html="setFlag(film.original_language)"></p>  
      <div>
        <!-- Ciclo per stampare le stelle per le serie TV -->
        <i v-for="n in 5" :key="n" class="fa-star" :class="(n <= getIntVote(serie.vote_average)) ? 'fas' : 'far' " ></i>
        </div>
    </li>
  </ul>
</template>

<style lang="scss" scoped>
</style>