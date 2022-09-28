<template>
<Navbar/>
  <router-view/>
</template>


<script>
// import { defineComponent } from '@vue/composition-api'
import Navbar from "./components/Navbar.vue"

export default ({
  components: {Navbar},
  // data() {
  //   return  null
  // },
})
</script>


<style>
#app {
 
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #555;
    max-width: 600px;
    margin:0 auto;
}
 body{
  margin: 0;
  padding: 0;
  background-color: #f2f2f2;
  
  }



</style>
