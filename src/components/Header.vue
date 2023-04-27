<template>
    <div class="header">
      <div class="card text-bg-dark">
        <router-link to="/movie/tt0409591">
          <img
            src="../assets/wallpapersden.com_anime-naruto-hd-2023-ai_1920x1080.jpg"
            alt="Naruto"
            class="card-img"
          />
          <div class="card-img-overlay">
            <h3 class="card-title">Naruto</h3>
            <p class="card-text">
              Naruto Uzumaki, a mischievous adolescent ninja, struggles as he
              searches for recognition and dreams of becoming the Hokage, the
              village's leader and strongest ninja.
            </p>
          </div>
        </router-link>
      </div>
    </div>
  </template>
  
  <script>

  export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name:"Header",
  };
  </script>
  <style lang="scss" scoped>
  .home {
    .card {
      color: #000;
      border-radius: 0 !important;
      --bs-card-inner-border-radius: 0;
      .card-img {
        height: 500px;
        object-fit: cover;
      }
      .card-img-overlay {
        top: auto;
        background-color: hsla(0, 0%, 0%, 0.582);
        color: #fff;
      }
      h3 {
        color: #fff;
      }
    }
  }
  </style>
  