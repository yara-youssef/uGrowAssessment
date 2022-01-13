<template>
  <RegistrationPage/>
</template>

<script>

import RegistrationPage from './pages/RegistrationPage.vue'

export default {
  name: 'App',
  components: {    
    RegistrationPage
  }
}
</script>

<style>
#app {
  font-family: Poppins, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-image: url(./assets/plantImage.jpg);
}
body{
  margin: 0;
}
</style>
