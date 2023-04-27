<template>
  <div class="home">
    <Header />
    <div class="container">
      <div class="row mt-4">
        <div class="d-flex justify-content-between flex-wrap">
          <div
            class="card m-1"
            style="width: 18rem"
            v-for="(movie, i) in movies"
            :key="i"
          >
            <img
              :src="`https://image.tmdb.org/t/p/original/${movie.poster_path}`"
              class="card-img-top"
              :alt="movie.original_title"
            />
            <div class="card-body d-flex justify-content-between flex-column">
              <h5 class="card-title">{{ movie.original_title }}</h5>
              <p class="card-text">{{ movie.overview }}</p>
              <router-link to="/movie/tt0409591" class="btn btn-detail w-100"
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
import { onMounted, ref } from "vue";
import axios from "axios";
export default {
  components: {
    Header,
  },

  setup() {
    const movies = ref([]);
    onMounted(async () => {
      const results = await axios.get(
        `https://api.themoviedb.org/3/movie/popular?api_key=${env.apikey}`
      );

      if (results.status == 200) {
        movies.value = results.data.results;
      }
    });

    return {
      movies,
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
