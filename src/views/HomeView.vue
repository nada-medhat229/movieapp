<template>
  <div class="home">
    <Header />
    <input
      type="text"
      class="form-control w-75 m-auto my-3"
      placeholder="What are you Looking For?"
      v-model="search"
    />
    <div class="container">
      <div class="row">
        <div class="col-md-3" v-for="(movie, i) in searchmovie" :key="i">
          <div class="card-movie">
            <img
              :src="`https://image.tmdb.org/t/p/original/${movie.poster_path}`"
              class="card-img-top"
              :alt="movie.original_title"
            />
            <div class="card-body d-flex justify-content-between flex-column">
              <h6 class="card-title">{{ movie.original_title }}</h6>
              <p class="card-text">{{ movie.overview }}</p>
              <router-link :to="'/movie/'+movie.id" class="btn btn-detail w-100"
                >Detail</router-link
              >
            </div>
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
        `https://api.themoviedb.org/3/movie/popular?api_key=${env.apikey}`
      );
      console.log(results);
      movies.value = results.data.results;

      if (results.status == 200) {
        movies.value = results.data.results;
      }
    });

    const searchmovie = computed(() => {
      return movies.value.filter((movie) => {
        return (
          movie.title.toLowerCase().indexOf(search.value.toLowerCase()) != -1
        );
      });
    });

    return {
      search,
      movies,
      searchmovie,
    };
  },
};
</script>
<style lang="scss" scoped>
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

  .card-movie {
    // background: #fff;
    color: #fff;
    margin: 10px 0;
    h6{
      display: -webkit-box;
      -webkit-box-orient: vertical;
      overflow: hidden;
      -webkit-line-clamp: 1;
    }
    .card-img-top {
      height: 350px;
      border-radius: 10px 10px 0 0;
    margin-bottom: 10px;
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
