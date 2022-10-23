<template>
<div class="min-h-full realitve bg-slate-800">
  
  <!--Hero section-->
  <HeroBanner />

  <!--Search section-->
  <div class="max-w-[1400px] mx-auto flex py-8 px-4">
    <input 
    v-model.lazy="searchInput" 
    type="text"
    placeholder="Search for movie" 
    class="max-w-[350px] w-full py-3 px-2 text-base border-none"
    @keyup.enter="$fetch"
      />
    <button 
    v-show="searchInput !== ''" 
    class="inline-block py-2 px-4 border-0 text-white rounded-md cursor-pointer hover:bg-yellow-700"
    @click="clearSearch"
      >
      Clear Search
    </button>
  </div>

  <!--Loading-->


  <!--Movies section-->
<div class="max-w-[1400px] mx-auto py-8 px-4">
  <!--Searched Movies-->
  <div 
    v-if="searchInput !== ''"
    id="movie-grid" 
    class="grid gap-x-8 gap-y-16 grid-cols-1
    sm:grid-cols-2
    md:grid-cols-2
    lg:grid-cols-4"
    >
    <div v-for="(movie, index) in searchedMovies" :key="index" class="relative flex flex-col">
      <div class="block w-full h-full">
        <img :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`" alt="" />
        <p 
          class="absolute top-0 left-0 flex justify-center items-center w-10 h-10 text-white 
          bg-red-600 rounded-t-none rounded-l-none rounded-r-lg rounded-b-lg"
          >
          {{ movie.vote_average }}</p>
        <!--<p 
          class="leading-normal absolute bottom-0 bg-amber-700 p-3 text-white 
           transition-transform duration-300 translate-y-3/4"
          >
          {{ movie.overview }}
        </p> -->
      </div>
      <div class="mt-auto">
        <p class="mt-2 text-white text-xl">{{ movie.title.slice(0, 25) }} 
          <span v-if="movie.title.length > 25">...</span>
        </p>
        <!--
        <p class="mt-2 text-gray-400">
              Released:
              {{
                new Date(movie.release_date).toLocaleString('en-us', {
                  month: 'long',
                  day: 'numeric',
                  year: 'numeric',
                })
              }}
        </p>
      -->
          <nuxt-link 
          class="inline-block py-2 px-4 border-0 text-white rounded-md cursor-pointer hover:bg-yellow-700"
          :to="{ name: 'movies-movieid', params: { id: movie.id } }"
          > Get more info</nuxt-link>
      </div>
    </div>
  </div>

  <!--Now Streaming-->
  <div 
    v-else
    id="movie-grid" 
    class="grid gap-x-8 gap-y-16 grid-cols-1
    sm:grid-cols-2
    md:grid-cols-2
    lg:grid-cols-4"
    >
    <div v-for="(movie, index) in movies" :key="index" class="relative flex flex-col">
      <div class="block w-full h-full">
        <img :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`" alt="" />
        <p 
          class="absolute top-0 left-0 flex justify-center items-center w-10 h-10 text-white 
          bg-red-600 rounded-t-none rounded-l-none rounded-r-lg rounded-b-lg"
          >
          {{ movie.vote_average }}</p>
        <!--<p 
          class="leading-normal absolute bottom-0 bg-amber-700 p-3 text-white 
           transition-transform duration-300 translate-y-3/4"
          >
          {{ movie.overview }}
        </p> -->
      </div>
      <div class="mt-auto">
        <p class="mt-2 text-white text-xl">{{ movie.title.slice(0, 25) }} 
          <span v-if="movie.title.length > 25">...</span>
        </p>
        <!--
        <p class="mt-2 text-gray-400">
              Released:
              {{
                new Date(movie.release_date).toLocaleString('en-us', {
                  month: 'long',
                  day: 'numeric',
                  year: 'numeric',
                })
              }}
        </p>
      -->
          <nuxt-link
          class="inline-block py-2 px-4 border-0 text-white rounded-md cursor-pointer hover:bg-yellow-700"
          :to="{ name: 'movies-movieid', params: { id: movie.id } }"
          > Get more info</nuxt-link>
      </div>
    </div>
  </div>
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
    }
  }
}
</script>
