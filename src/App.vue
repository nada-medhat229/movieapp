<template>
  <div>
    <Nav/>
  <main class="">
    <router-view/>
  </main>
  </div>
</template>
<script>
import Nav from './components/Nav.vue';
export default{
  components:{
    Nav
  }
}
</script>
<style lang="scss">
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Fira Sans',sans-serif;
  &::selection{
    background: transparentize( #ab00d8, 0.5);
  }
}
body{
background-color: #000000f5 !important;
color: #fff !important;
}
a{
  text-decoration: none !important;
}
</style>
