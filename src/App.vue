<template>
  <div id="app">
    <app-header></app-header>
   <router-view></router-view>
  </div>
</template>

<style>

</style>

<script>
  import addBlog from './components/addBlog.vue'
  import showBlogs from './components/showBlogs.vue'
  import header from './components/header'
  export default {
    components: {
      'add-blog': addBlog,
      'show-blogs': showBlogs,
      'app-header': header
    },

    data () {

      return {

      }

    },

    methods: {

    }
  }
</script>

<style>
  body{
    margin: 0;
    font-family: 'Nunito SemiBold';
  }
</style>
