<template>
  <div class="home">
    <div class="feature-card">
      <router-link to="/movie/tt0126029">
        <img src="https://images.gmanews.tv/webpics/2021/06/Poster1-Rick_and_Morty_S5-HBO_GO_2021_06_08_15_28_09.jpg" alt="Rick&Morty Poster" class="featured-img">
      <div class="detail">
       
        <h3>Watch Season 6 Now</h3>
        <p>Brilliant but boozy scientist Rick hijacks his fretful teenage
        <br>grandson, Morty, for wild escapades in other worlds and
        <br>alternate dimensions. </p>
      </div>
      </router-link>
    </div>

    <form @submit.prevent="SearchMovies()" class="search-box">
      <input type="text" placeholder="Titles, people, genres" v-model="search" />
      <input type="submit" value="Search" />
    </form>

    <div class="movies-list">
      <div class="movie" v-for="movie in movies" :key="movie.imdbID">
        <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
          <div class="product-image">
            <img :src="movie.Poster" alt="Movie Poster" />
            <div class="type">{{ movie.Type }}</div>
          </div>
          <div class="detail">
            <p class="year">{{ movie.Year }}</p>
            <h3>{{ movie.Title }}</h3>
          </div>

      </router-link>
    </div>
  </div>
  </div>
</template>

<script>
 import { ref } from 'vue';
import env from '@/env.js'
export default {
  setup () {
    const search = ref("");
    const movies = ref([]);
    const SearchMovies = () => {
      if (search.value != "") {
        fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
          .then(response => response.json())
          .then(data => {
            movies.value = data.Search;
            search.value = "";
          });
      }
    }
    return {
      search,
      movies,
      SearchMovies
    }
  }
}
</script>

<style lang="scss">
.home {
  .feature-card {
    position: relative;
    .featured-img {
      display: block;
      width: 100%;
      height: 300px;
      object-fit: cover;
      position: relative;
      z-index: 0;
    }
    .detail {
      position: absolute;
      text-shadow: 1.2px 1.2px #000000;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: transparent;
      padding: 16px;
      z-index: 1;
      h3{
            color: white;
            margin-bottom: 16px;
            opacity: 95%;
          }

          p{
            color: white;
            opacity: 95%;
            
      }
    }
  }

  
  .search-box {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 16px;
    input {
      display: block;
      appearance: none;
      border: none;
      outline: none;
      background: none;
      &[type="text"] {
        width: 100%;
        color: #FFF;
        background-color: black;
        font-size: 20px;
        padding: 10px 16px;
        border-radius: 8px;
        margin-bottom: 15px;
        transition: 0.4s;
        &::placeholder {
          color: #b0b0b0;
        }
        &:focus {
          box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.2);
        }
      }
      &[type="submit"] {
        width: 100%;
        max-width: 300px;
        background-color: #000000;
        padding: 16px;
        border-radius: 8px;
        color: #FFF;
        font-size: 20px;
        text-transform: uppercase;
        transition: 0.4s;
        &:active {
          background-color: #ff0000;
        }
      }
    }
  }
  .movies-list {
    display: flex;
    flex-wrap: wrap;
    margin: 0px 8px;
    .movie {
      max-width: 50%;
      flex: 1 1 50%;
      padding: 16px 8px;
      .movie-link {
        display: flex;
        flex-direction: column;
        height: 100%;
        .product-image {
          position: relative;
          display: block;
          img {
            display: block;
            width: 100%;
            height: 275px;
            object-fit: cover;
          }
          .type {
            position: absolute;
            padding: 8px 16px;
            background-color: #252525;
            color: #FFF;
            bottom: 16px;
            left: 0px;
            text-transform: capitalize;
            opacity: 70%;
          }
        }
        .detail {
          background-color: #181818;
          padding: 16px 8px;
          flex: 1 1 100%;
          border-radius: 0px 0px 8px 8px;
          .year {
            color: #AAA;
            font-size: 14px;
          }
          h3 {
            color: #FFF;
            font-weight: 600;
            font-size: 18px;
          }
        }
      }
    }
  }
}
</style>