<template>
  <div class="home">
    <div class="fature-card">
      <router-link to="/movie/tt0409591">
        <img class="fature-img" src="https://m.media-amazon.com/images/M/MV5BMDI3ZDY4MDgtN2U2OS00Y2YzLWJmZmYtZWMzOTM3YWFjYmUyXkEyXkFqcGdeQXVyNjAwNDUxODI@._V1_SX300.jpg" alt="Naruto Poster">
        <div class="detail">
          <h3>Naruto</h3>
          <p>Many years ago, in the hidden village of Konoha, lived a great demon fox. When it swung one of it's nine tails, a tsunami occurred. The fourth hokage sealed this demon fox inside a boy in exchange for his own life. Naruto was that boy, and he grew up with no family, and the villagers hated him thinking that he himself was the demon fox. Naruto's dream is to become Hokage, and have the villagers acknowledge him.</p>
        </div>
      </router-link>
    </div>

      <form action="" @submit.prevent="searchMovie()" class="search-form">
        <input type="text" placeholder="What do you looking for?" v-model="search">
        <button>Search</button>
      </form>

      <div class="movie-list">
          <div class="movie" v-for="movie in movies" :key="movie.imdbID">
            <router-link class="movie-link" :to="'/movie/' + movie.imdbID" >
              <div class="product">
                <div class="product-img"><img :src="movie.Poster" :alt="movie.Title"></div>
                <div class="product-type">{{ movie.Type }}</div>
              </div>
              <div class="det">
                <div class="det-year">{{ movie.Year }}</div>
                <div class="det-title">{{ movie.Title }}</div>
              </div>
            </router-link>
          </div>
      </div>
  </div>
    
      <!-- <p>{{ movies }}</p> -->
    
  
</template>

<script>
import { ref } from 'vue'
// import env from 'vue'

// @ is an alias to /src

export default {
  setup(){
    let movies = ref([])
    let search = ref("")
    function searchMovie(){
      if(search.value != "")
      console.log(search.value);
      fetch(`http://www.omdbapi.com/?apikey=d973bb6f&s=${search.value}`)
      .then(response => response.json())
      .then(data=>{
        movies.value = data.Search
        console.log(movies.value);
        search.value = ""
      })
    }
    return{search, searchMovie,movies}
  }
}
</script>

<style lang="scss">
.home .fature-card{
  position: relative;

}
.home .fature-img{
  width: 50%;
  display: block;
  height: 500px;
  margin: 0 auto;
}
.home .fature-card .detail{
  position: absolute;
  background-color: rgba(0, 0,0, 0.6);
  left:0px;
  right:0px;
  bottom:0px;
  padding: 16px;
  z-index: 1;
  width: 50%;
  margin: 0 auto;
  color: white;
}
.home .fature-card .detail p{
  padding-top: 20px;
  line-height: 22px;
}
form input {
  width: 50%;
  height: 3rem;
  display: block;
  border-radius: 10px;
  border: none;
  background:#496586;
  margin: 10px;
  outline: none;
  padding: 10px;
  margin: 20px auto;
}
form input::placeholder {
  color: rgb(233, 233, 233);
  font-size: 18px;
}
form button {
  padding: 15px 50px;
  border-radius: 10px;
  border: none;
  cursor: pointer;
  margin:10px ;
  margin: 0 auto;
  display: block;
  background:#428883 ; 
  font-size: 18px;
  color: white; 
}
form button:active{
  background: #388070;
}
.movie-list{
  display: grid;
  grid-template-columns: repeat(3,1fr);
  // justify-content: space-between;
  // align-items: ;
  width:fit-content;
  margin: 20px auto;



}

.movie {
  // border: 2px solid green;
  margin: 20px auto;
  max-width: 75%;

  
}

.movie-link{
  // border: 1px solid black;
  display: flex;
  flex-direction: column;
  // height: 100%;
  position: relative;

  
}
.product{
  align-items: center ;
  // border: 2px solid chocolate;
  width: 100%;
  height: 100%;

}

.product-type{
  position: absolute;
  top:0;
  left: 0;
  bottom: 40;
  z-index: 1;
  color: white;
  background-color: #428883;
  padding: 10px 20px;

}
.det{
  // border: 2px solid blue;
  padding-top: 0px;
}
.det .det-year{
  color: rgba(255, 255, 255, 0.5);
  padding: 10px 0;
}

.det .det-title{
  // color: rgba(255, 255, 255, 0.5);
  padding-bottom: 10px;
  // word-wrap: break-word;
  word-break: break-all;
  color: white;


}

</style>

