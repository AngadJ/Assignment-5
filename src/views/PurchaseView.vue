<script setup>
import SiteFooter from "../components/SiteFooter.vue";
import axios from "axios";
import { ref } from 'vue';
import SiteModal from '../components/SiteModal.vue';
const showModal = ref(false);
const selectedId = ref(0);
const openModal = (id) => {
  showModal.value = true;
  selectedId.value = id;
};
const closeModal = () => {
  showModal.value = false;
};
let data = (await axios.get("https://api.themoviedb.org/3/trending/movie/week", {
    params: {
        api_key: "f944b70daa59b60504fca0c383e63483"
    }
})).data.results;
console.log(data)
</script>

<template>
   <div>
      <h1> Wondering what movie to watch next? <br> Here are the current trending movies, click on the movie to get some cool info!</h1>
 
    </div>

    <div>
        <img v-for="movie in data" @click="openModal(movie.id)" class="poster" :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`" alt="">
    </div>
    <SiteModal v-if="showModal" @toggleModal="closeModal()" :id="selectedId" />
    <div>
        <SiteFooter />
    </div>
</template>

<style scoped>
 h1 {
    color: white;
    border-color: rgb(58, 186, 237);
    border-width: 15px;
    border-style: double;
    font-family: 'Zen Dots', cursive;
    padding: 20px;
    font-size: 25px;
   }
   
   :hover {
    border-width: 15px;
    border-color: white
 
  }
img {
  width: 270px; 
  border-style: double;
  border-color: rgb(58, 186, 237);
  border-width: 15px;
  margin-right: 10px;
  margin-top: 15px;
}

.footer {
  font-size: 15px;
  font-family: 'Play', sans-serif;
  text-align: center;
  padding: 3px;
  background-color: rgb(58, 186, 237);
  color: navy;
  position: relative;
  bottom: -10px;
  
}
</style>