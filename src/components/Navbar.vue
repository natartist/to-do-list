<template>
<!--nav.navbar.navbar-light.bg-light>.container-fluid>span.navbar-brand.mb-0.h1
You-->


  <nav class="navbar-navbar-light bg-light">
    <div class="container-fluid"><span class="navbar-brand">Organizador de tareas</span></div>
  </nav>
</template>

<script>
export default {

}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Quicksand:wght@300&display=swap');

.container-fluid {
  height: 45px;
  position: relative;
}

.navbar {
  box-shadow:  0 0px 10px 0 rgba(0,0,0,0.4);
  
}

.navbar-brand {
/* font-family: 'Quicksand', sans-serif; */
font-family: 'Roboto Mono', monospace;
color: gray;
position: absolute;
top: 6px;
}
</style>