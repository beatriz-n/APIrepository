<template>
  <div>
    <br>
    <img alt="Vue logo" src="https://icones.pro/wp-content/uploads/2021/06/symbole-github-violet.png">
    <repo-comp></repo-comp>

  </div>
 
</template>

<script>
import RepoComp from './components/repoComp.vue'
//import axios from 'axios';
export default {
  name: 'App',
  components: {
    RepoComp
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
*{
  background-color:#0d1116 ;
}
img{
  width: 5%;
}
</style>
