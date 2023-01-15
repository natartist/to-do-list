<template>
<div class="fondo mb-5">
 <Navbar/>
 <Tarea/>
</div>
 
</template>

<script>
import Navbar from '@/components/Navbar.vue';
import Tarea from "./components/Tarea.vue"

export default {
  name: 'App',
  components: {
    Navbar,
    Tarea 
  }
}
</script>

<style>
.fondo {
  /* background-image: url("./assets/lineas.jpg"); */
  background-size: cover;
   /* background-size: contain; 
  background-position: center center;
  background-repeat: no-repeat; */

  /* height: 100vh; */

}

</style>
