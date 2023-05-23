<template lang="">
  <div class="container">
    <div class="card border-0 ">
    <img
      :src="`https://image.tmdb.org/t/p/original/${movie.poster_path}`"
      class="card-img-top poster"
      :alt="movie.original_title"
    />
    <div class="card-body">
      <h4 class="card-title">{{ movie.original_title }}</h4>
      <p class="card-date">{{ movie.release_date }}</p>

      <p class="card-text">{{ movie.overview }}</p>
    </div>   
    <div class="row">
      <h4>production companies:</h4>
      <div
        class="col-md-4 h-100"
        v-for="(production,ii) in movie.production_companies"
        :key="ii"
      >
        <div class="card production">
          <img
            :src="`https://image.tmdb.org/t/p/original/${production.logo_path}`"
            class="card-img-top"
            :alt="production.name"
          />
          <div class="card-body">
            <h5 class="card-title">{{ production.name }}</h5>
            <p class="card-text">
              {{production.origin_country}}
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
  </div>
</template>
<script>
// import env from "../env";
import axios from "axios";
import { ref, onBeforeMount } from "vue";
import { useRoute } from "vue-router";
export default {
  setup() {
    const movie = ref({});
    const route = useRoute();
    const options = {
      method: "GET",
      headers: {
        accept: "application/json",
        Authorization:
          "Bearer eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiI5ZTBhMTA2YTkzOWQzNTRkYmU3MDUxOWUwMDY2NzJiZCIsInN1YiI6IjYyNDQ3OGFmYzUwYWQyMDA1Y2RmZmYwOSIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.wIF5o9MKFdHLWxFR_64NzinOyrPS6f4uLiNiIPY0eQI",
      },
    };
    onBeforeMount(async () => {
      const results = await axios.get(
        `https://api.themoviedb.org/3/movie/${route.params.id}`,
        options
      );
      console.log(results.data, route.params.id);
      if (results.status == 200) {
        movie.value = results.data;
      }
    });
    return {
      movie,
    };
  },
};
</script>
<style lang="scss" scoped>
.card{
  background: transparent;
  .poster{
    height: 95vh;
  }
  .card-title{
    color: #ea813b;
  }
  .card-date{
    background: #ea813b;
    color: #fff;
    border-radius: 25px;
    padding: 12px;
    width: max-content;
  }
}
.production img{
  width: 100%;
  height: 200px;
  background: #fff;
  padding: 20px;
}
</style>
