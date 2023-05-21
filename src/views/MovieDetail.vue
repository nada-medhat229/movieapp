<template lang="">
    <div>
        <h2>movie title</h2>
    </div>
</template>
<script>
// import env from "../env";
import axios from 'axios';
import {ref,onBeforeMount} from 'vue';
import { useRoute } from 'vue-router';
export default {
    setup(){
        const movie=ref({});
        const route=useRoute();
        const options = {
  method: 'GET',
  headers: {
    accept: 'application/json',
    Authorization: 'Bearer eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiI5ZTBhMTA2YTkzOWQzNTRkYmU3MDUxOWUwMDY2NzJiZCIsInN1YiI6IjYyNDQ3OGFmYzUwYWQyMDA1Y2RmZmYwOSIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.wIF5o9MKFdHLWxFR_64NzinOyrPS6f4uLiNiIPY0eQI'
  }
};
        onBeforeMount(async()=>{
            const results = await axios.get(
                `https://api.themoviedb.org/3/movie/${route.params.id}`,options)
console.log(results,route.params.id);
      if (results.status == 200) {
        movie.value = results.data;
      }
        })
        return {
            movie
        }
    }
}
</script>
<style lang="">
    
</style>