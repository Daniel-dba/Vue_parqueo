<template>
<h1>EMPLEADO   Editar</h1>

<div class="container">
        <h5>Empleado Editar</h5>
    
        <div class="card">
            <div class="card-content">
              <form @submit.prevent="update()">
                <p>Nombre: <input type="text" v-model = "payload.nombre"  required/></p>
                <p>Area: <input type="text" v-model = "payload.area"  required/></p>
                <p>Movilidad: <input type="text" v-model = "payload.movilidad"  required/></p>
                <p>Placa: <input type="text" v-model = "payload.placa"  required/></p>
                <p>Color: <input type="text" v-model = "payload.color"  required/></p>
                    <p>
                        <!-- <label>
                          <input type="checkbox" class="filled-in" v-model="payload.movilidad" />
                          <span>Movilidad</span>
                        </label> -->
                    </p>
                    <button type="submit" class="waves-effect waves-light btn-small">Editar</button>
                </form>
            </div>
        </div>
    
    </div>





</template>

<script>

export default {
  name: 'EmpleadoView',
  data(){
    const api = process.env.VUE_APP_API;
    return{
      api,
      items: [],
      payload:{
        nombre: null,
        area: null,
        movilidad: null,
      }
    }
  },
  methods:{
    getOne(){
      this.axios({
        method: 'get',
        url: this.api + '/empleado/' + this.$route.params.id,
      })
      
      .then((response)=>{
      this.payload = response.data;
       })
      .catch((error)=>{
      console.log(error)
      })
    },
update(){
  if(confirm("Esta seguro de editar?")){
    console.log(this.$route.params)
  this.axios.patch(this.api + '/empleado/' + this.$route.params.id, this.payload)
      
      .then((response)=>{
         console.log(response);
       })
      .catch((error)=>{
      console.log(error)
      })
    }      
},

  },
  components: {
  },
  mounted(){
   this.getOne();
  }
}
</script>
