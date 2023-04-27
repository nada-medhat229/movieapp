<template>
    <div class="home">
      <Header />
      <form action="" class="d-flex justify-content-between">
        <input
          type="text"
          class="form-control w-75"
          placeholder="What are you Looking For?"
          v-model="search"
        />
      <button  @click="searchmovie()"> search</button>
      </form>
      <div class="container">
        <div class="row">
          <div class="d-flex justify-content-between flex-wrap">
            <div
              class="card m-1"
              style="width: 18rem"
              v-for="(movie, i) in movies"
              :key="i"
            >
           {{ movie }}
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import Header from "@/components/Header.vue";
  import env from "../env";
  import { computed, onMounted, ref } from "vue";
  import axios from "axios";
  export default {
    components: {
      Header,
    },
  
    setup() {
      let search = ref("");
      let movies = ref([]);
      onMounted(async () => {
        const results = await axios.get(
        `https://api.themoviedb.org/3/search/movie?api_key=${env.apikey}&query=${search.value}`
        );
        movies.value = results.data.results;
  
        if (results.status == 200) {
          movies.value = results.data.results;
        }
      });
      const searchmovie = computed(() => {
        let filter = search.value;
        return movies.value.filter((movie) => {
          movie.title.toLowerCase().includes(filter.toLowerCase());
        });
      });
      console.log(searchmovie);
      return {
        search,
        movies,
        searchmovie,
      };
    },
  };
  </script>
  <style lang="scss">
  .home {
    form {
      padding: 16px;
      input {
        border: none;
        padding: 10px 16px;
        margin: 0 10px;
        &[type="submit"] {
          background: #ea813b;
          color: #fff;
          &:active {
            background: #ea813bc8;
          }
        }
        &:focus {
          box-shadow: none;
        }
      }
    }
  
    .card {
      color: #000;
      .card-img-top {
        height: 350px;
      }
      .card-text {
        display: -webkit-box;
        -webkit-box-orient: vertical;
        overflow: hidden;
        -webkit-line-clamp: 3;
        color: #818181;
        line-height: 1.8;
      }
      .btn-detail {
        background: #ea813b;
        color: #fff;
        &:hover {
          background: #ea813bc8;
          color: #fff;
        }
      }
    }
  }
  </style>
  