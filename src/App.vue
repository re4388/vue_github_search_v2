<template lang='pug'>
 #app
  b-container
    header
      a(href='https://github.com/')
        img(src='./assets/github_small.png', alt='Github small logo')
      b-nav.m-3(align='fixed-top')
        b-nav-item(active='')
          router-link(:to="{ name: 'Hello' }") Home
        b-nav-item(active='')
          router-link(to='/about') About
        b-nav-item(active='')
          router-link(to='/repos') Repos Fast Look
    main
      router-view
</template>

<script>
// import dotenv from "dotenv";
// require('dotenv').config()


export default {
  name: "app",
  data() {
    return {
      // userId: ""
    };
  },
  mounted() {
    console.log(process.env.VUE_APP_GITHUB_USER_NAME);
    console.log(process.env.VUE_APP_GITHUB_PASSWROD);
    // console.log();
    
  },
  // watch: {
  //   $route: function() {
  //     this.userId = this.$router.history.current.params.id
  //   }
  // }
};
</script>

<style lang="scss" scoped>
html {
  height: 100%;
  background: #63d0ff;
}
body {
  font-family: "Montserrat", sans-serif;
  margin: 0;
  padding: 0;
  background: #63d0ff;
  height: 100%;
}
</style>