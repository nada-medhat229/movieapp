<template>
    <div class=" nav justify-content-center">
        <router-link to="/">
            <h1><span>APP </span> Movies</h1>
        </router-link>
    </div>
</template>
<script>
export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name:"Nav",
}
</script>
<style lang="scss">
.nav{
    background-color: #000000 ;
    h1{
        padding: 10px 16px;
        color: #fff;
        span{
            color: #ea813b;
        }
    }}
</style>