<template>
<div class="min-h-full realitve bg-slate-800">
  
  <!--Hero section-->
  <HeroBanner />

  <!--Search section-->
  <SearchBar :model-value="searchInput" @submitted="submitSearch" @clear="clearSearch" /> 
   

  <!--Loading-->


  <!--Movies section-->
<div class="max-w-[1400px] mx-auto py-8 px-4">
 
  <!--Searched Movies-->
  <template  v-if="searchInput !== ''">
      <MovieList :movies="searchedMovies" /> 
  </template>
 
  <!--Now Streaming-->
  <template v-else>
    <MovieList :movies="movies" /> 
  </template>

</div>

</div>
</template>

<script>
import axios from 'axios';
import HeroBanner from '../components/HeroBanner.vue';
export default {
  name: "IndexPage",
  components: { HeroBanner },
  data(){ 
    return{
      movies:[],
      searchedMovies: [],
      searchInput: '',
    }
  },
  async fetch() {
    if(this.searchInput === '') {
      await this.getMovies()
      return
    }
    
    await this.searchMovies()
   
  },
  methods: {
    async getMovies(){
      const data = axios.get('https://api.themoviedb.org/3/movie/now_playing?api_key=37ed43a4f8eaa2abd75f9283692947bc&language=en-US&page=1')
      const result = await data
      result.data.results.forEach(movie => {
        this.movies.push(movie)
      })
    },
    async searchMovies () {
      const data = axios.get(
        `https://api.themoviedb.org/3/search/movie?api_key=37ed43a4f8eaa2abd75f9283692947bc&language=en-US&page=1&query=${this.searchInput}`
      )
      const result = await data
      result.data.results.forEach( movie => {
        this.searchedMovies.push(movie)
      })
    },
    clearSearch() {
      this.searchInput = ''
      this.searchedMovies = []
    },
    submitSearch(value) {
        this.searchInput = value
        this.$fetch()
    }
  }
}
</script>
