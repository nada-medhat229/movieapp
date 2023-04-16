<template>
    <div class="text-center header">
        <router-link to="/">
            <h1><span>APP </span> Movies</h1>
        </router-link>
    </div>
</template>
<script>
export default {
    // eslint-disable-next-line vue/multi-word-component-names
    name:"Header",
}
</script>
<style lang="scss">
.header{
    background-color: #000000 ;
    h1{
        padding: 10px 16px;
        color: #fff;
        span{
            color: #ab00d8;
        }
    }}
</style>