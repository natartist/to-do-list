<template>
  <div class="container mt-3 mb-5">
    <div class="row">
     
      <div class="ingresa-tarea col-8 mt-3">
        <input 
        class="form-control" 
        type="text" 
        placeholder="Ingresa una tarea"
        v-model="nombreTarea"
        @keyup.enter="agregarTarea"
      />
      </div>
      

     <div class="sin-tareas col-8 "> 
    <div v-if="tareas.length === 0" class="card p-2 alert alert-warning">
      <h6 class="">No hay tareas para mostrar...</h6>
    </div>
<!--Aquí vamos a renderizar nuestras tareas-->
<ul class="list-group">
  <li v-for="(tarea, index) of tareas" :key="index" class="list-group-item d-flex justify-content-between align-items-center">
    <span class="cursor" @click="actualizarTarea(tarea, index)">
      <i :class="tarea.estado?'fas fa-check-circle text-success':'far fa-circle'"></i>
    </span>
    <h5>{{ tarea.nombre }}</h5>
    <span class="cursor text-danger" @click="eliminarTarea(index)">
      <i class="fa fa-trash-alt"></i>
    </span>
  </li>
</ul>
     </div>
     

    </div>
    <br>
  
      </div>
</template>

<script>
export default {
  data() {
    return {
      tareas: [],
      nombreTarea: ""
    }
  },
  methods: {
    agregarTarea() {
      if(this.nombreTarea === "") {
        this.$swal.fire({
          title: "Debes crear una tarea",
          showClass: {
            popup: "animate__animated animate__fadeInDown"
          },
          hideClass: {
           popup: "animate__animated animate__fadeOutUp"
           }
        });
        return;
      }
      //console.log("AGREGANDO UNA TAREA...");

      // Nuestra tarea
      const tareaObject = {
        nombre: this.nombreTarea,
        estado: false
      }
      this.nombreTarea = "";
      //console.log(tareaObject);
      this.tareas.push(tareaObject);
      console.log(this.tareas);
      localStorage.setItem("tareas-storage", JSON.stringify(this.tareas));
     
    },
    eliminarTarea(indice) {
      this.$swal.fire({
  title: '¿Estás seguro?',
  text: "¡No podrás revertir esto!",
  icon: 'warning',
  showCancelButton: true,
  confirmButtonColor: 'rgb(206, 115, 130)',
  // cancelButtonColor: 'rgb(147, 192, 147)',
  confirmButtonText: '¡Eliminar tarea!',
  customClass: 'custom-swal'
}).then((result) => {
  if (result.isConfirmed) {

    this.tareas.splice(indice, 1);
    //en este punto tenemos un arreglo con las tareas eliminadas
    //y ahora actualizamos el localstirage con la tarea que se eliminó
    localStorage.setItem("tareas-storage", JSON.stringify(this.tareas));
    Swal.fire(
      '¡Eliminada!',
      'Tu tarea ha sido eliminada.',
      'success'
    )
  }
});
    //tareas [ "ble", "bli", "blu"]
    //indice indicamos donde querwmos empezar a eliminar  y con el 1 ctos elementos a eliminar
    
    }, 
    actualizarTarea(tarea, indice) {
      this.tareas[indice].estado = !tarea.estado; // tarea.estado está en false
      localStorage.setItem("tareas-storage", JSON.stringify(this.tareas))
    console.log(this.tareas);
    }
  },
  created() {
    //llamar la información que existe dentro del local storage
    if(localStorage.getItem("tareas-storage")) {
      console.log("Existe informacion en el local storage");
      this.tareas = JSON.parse(localStorage.getItem("tareas-storage"));
    }
  }

};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Roboto+Mono&display=swap');
/* @import url('https://fonts.googleapis.com/css2?family=Quicksand:wght@300&display=swap'); */

.row {
   background-image: url("../assets/fondo2.jpeg");
   /* background-size: cover; */
   /* background-size: contain; 
  background-position: center center;
  background-repeat: no-repeat; */
   height: 640px;
   width: 965px;
   /* margin-bottom: 100px !important;
   margin-right: 0px !important; */
   display: flex;
   justify-content: center;
   margin-left: 80px !important;
   border-radius: 30px;
   /* background: #EBCED0;*/
   box-shadow: 10px 10px 15px -3px rgba(125,123,125,0.79);
   position: relative;
}

.col-8 {
  position: absolute;
  left: 10px;

}
.sin-tareas {
  position: absolute;
  top: 60px;

}

.form-control {
  border-radius: 13px !important;
  /* font-family: 'Quicksand', sans-serif; */
  font-family: 'Roboto Mono', monospace;
  color: gray;
}
.card {
  border-radius: 13px !important;
  /* font-family: 'Quicksand', sans-serif; */
  font-family: 'Roboto Mono', monospace;
  color: gray;
 
}
.alert.alert-warning {
   background-color: #ffff;
   color: gray;
   /* border-color: #ffff; */
   border: 1px solid #ced4da;
}
.custom-swal {
  border-radius: 40px;
}

.fa.fa-trash-alt
{
  color:rgb(206, 115, 130);
}

.far.fa-circle {
  color: rgb(166, 213, 166);
}

.text-success {
  color: rgb(147, 192, 147) !important;
}

.list-group-item {
/* font-family: 'Quicksand', sans-serif; */
font-family: 'Roboto Mono', monospace;
color: gray;

}
.cursor {
  cursor:pointer;
}

</style>