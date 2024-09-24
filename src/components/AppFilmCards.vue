<script>
export default {
  data() {
    return {
      
    }
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
        <span v-if="getIntVote(film.vote_average === 0)">
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

<style scoped>
</style>