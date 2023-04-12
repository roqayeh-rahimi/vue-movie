<template>
  <!-- <h1>Movie Detail </h1> -->
  <div class="movie-content">
    <h2>{{ movies.Title}}</h2>
    <h4>{{ movies.Year }}</h4>
    <img :src="movies.Poster" :alt="movies.Title">
    <p>{{ movies.Plot }}</p>
  </div>

</template>

<script>

import { ref ,onBeforeMount } from 'vue'
import { useRoute } from 'vue-router'

export default {
  setup(){
    let movies = ref({})
    let route = useRoute()
    onBeforeMount(()=>{
      console.log("Before mount");
      fetch(`http://www.omdbapi.com/?apikey=d973bb6f&i=${route.params.id}&plot=full`)
      .then(response => response.json())
      .then(data => {
        movies.value = data
        console.log(movies.value);
      })
    })
    
    return{movies }
  }
}
</script>

<style>
.movie-content{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  color: white;
  /* text-align: center; */
  width: 50%;
  margin: 0 auto;
}
.movie-content h2{
  margin:15px;
  text-align: center; 
}
.movie-content h4{
  margin-bottom: 5px;
  font-size: 15px;
}
.movie-content p{
  margin-top: 20px;
  line-height: 23px;
}
@media (max-width < 500){
  .movie-content h2{
    font-size:10px ;
  }
}

</style>