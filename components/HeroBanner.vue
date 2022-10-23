<template>
  <div class="h-[400px] relative md:h-[500px]">
    <img src="../assets/images/hero-banner.jpg" alt="movie-banner" class="w-full h-full object-cover" />
  <div class="z-50 absolute top-0 m-0 w-full h-full flex flex-col justify-center text-white">
    <div class="px-[16px] w-full max-w-[1400px] mx-auto">
        <span class="font-semibold text-lg uppercase mb-2 md:text-xl">Now Streaming</span>
        <h1 class="text-6xl font-extralight mb-2 md:text-8xl"><span class="font-medium">Now</span> Streaming</h1>
        <a href="#movie-grid" class="text-xl self-start inline-block py-2 px-4 bg-red-600 rounded cursor-pointer">View Movies</a>
    </div>
  </div>
  </div>
</template>

<script>
export default {
    name: 'HeroBanner',
    
}
</script>

<style>

</style>