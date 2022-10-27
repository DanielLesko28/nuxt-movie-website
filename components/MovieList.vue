<template>
    <div 
    class="grid gap-x-8 gap-y-16 grid-cols-1
    sm:grid-cols-2
    md:grid-cols-2
    lg:grid-cols-4"
    >
    <div v-for="(movie, index) in movies" :key="index" class="relative flex flex-col">
      <div class="block w-full h-full overflow-hidden relative group">
        <img :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`" alt="" />
        <p 
          class="absolute top-0 left-0 flex justify-center items-center w-10 h-10 text-white 
          bg-red-600 rounded-t-none rounded-l-none rounded-r-lg rounded-b-lg"
          >
          {{ movie.vote_average }}</p>
         <p 
          class="leading-normal absolute bottom-0 bg-amber-700 p-3 text-white 
           transition-transform duration-300 translate-y-full group-hover:translate-y-0"
          >
          {{ movie.overview }}
        </p> 
      </div>
      <div class="mt-auto">
        <p class="mt-2 text-white text-xl">{{ movie.title.slice(0, 25) }} 
          <span v-if="movie.title.length > 25">...</span>
        </p>
        </div>
        
        <p v-if="movie.release_date" class="mt-2 text-gray-400">
              Released:
              {{
                new Date(movie.release_date).toLocaleString('cz-cs', {
                  month: 'long',
                  day: 'numeric',
                  year: 'numeric',
                })
              }}
        </p>
      
          <nuxt-link
          class="inline-block py-2 px-4 border-0 text-white rounded-md cursor-pointer hover:bg-yellow-700"
          :to="'/movies/' + movie.id"
          > Get more info</nuxt-link>
      
    </div>
  </div>
</template>

<script>
export default {
    props:{
        movies: {
            type: Array,
            default: () => []
        }
    }


}
</script>

<style>

</style>