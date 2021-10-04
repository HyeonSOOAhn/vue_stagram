<template>
  <div>
    <Post v-for="data in datas" :key="data" :data="data"/>
  </div>
</template>

<script>
import Post from './Post.vue';

export default {
    name : "Container",
    props : {
        datas : Array,
    },
    components : {
        Post,
    },

};
</script>

<style>
</style>