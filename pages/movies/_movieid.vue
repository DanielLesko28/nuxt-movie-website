<template>
  <div 
  class="max-w-[1400px] mx-auto text-white min-h-screen flex flex-col justify-center 
  single-movie"
  >
    <nuxt-Link class="self-start mb-8 p-3 bg-red-500 rounded-xl" :to="{ name: 'index'}">Back</nuxt-link>
    <div class="flex flex-col items-center gap-8 md:flex-row md:items-start">
        <div class="max-h-[500px] w-full md:max-h-[700px] md:w-fit">
            <img
            :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`"
            alt="" 
            class="max-h-[500px] w-full md:max-h-[700px] md:w-fit"
            /> 
        </div>
        <div class="text-14 font-medium">
            <h1>Title: {{ movie.title }}</h1>
            <p class="mt-3 text-xl leading-normal italic">
                <span class="font-semibold semibold">Tagline:</span>"{{movie.tagline}}"
            </p>
            <!--
            <p class="text-14 font-medium">
                <span>Released:</span>
                {{
                new Date(movie.release_date).toLocaleString('en-us', {
                  month: 'long',
                  day: 'numeric',
                  year: 'numeric',
                })
                }}
            </p>
            -->
            <p class="mt-3 text-xl leading-normal">
                <span>Duration:</span> {{movie.runtime}} minutes
            </p>
            <!--
            <p class="mt-3 text-xl leading-normal">
                <span>Revenue:</span>
                {{
                movie.revenue.toLocaleString('en-us', {
                style: 'currency',
                currency: 'USD',
                })
                }}
            </p>
        -->
            <p class="mt-3 text-xl leading-normal">
                <span>Overview:</span>{{ movie.overview }}
            </p>
        </div>
    </div>
  </div>
</template>

<script>
import axios from "axios"
export default {
    name: 'SingleMovie',
    data() {
        return {
            movie: '',
        }
    },
    async fetch() {
        await this.getSingleMovie()
    },
    methods: {
        async getSingleMovie() {
            const data = axios.get(`https://api.themoviedb.org/3/movie/${this.$route.params.movieid}?api_key=37ed43a4f8eaa2abd75f9283692947bc&language=en-US`)
            const result = await data
            this.movie = result.data
        }
    }
}
</script>

<style>

</style>