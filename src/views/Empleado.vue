<template>
<h1>EMPLEADO</h1>

<div class="container">
  <h5>Empleado</h5>
  <div class="card">
            <div class="card-content">
                <form @submit.prevent="nuevo()">
                  <p>Nombre: <input type="text" v-model = "payload.nombre"  required/></p>
                  <p>Area: <input type="text" v-model = "payload.area"  required/></p>
                  <p>Movilidad: <input type="text" v-model = "payload.movilidad"  required/></p>
                  <p>Placa: <input type="text" v-model = "payload.placa"  required/></p>
                  <p>color: <input type="text" v-model = "payload.color"  required/></p>
                  <button type="submit">Agregar</button>
                </form>

 <!--               <form @submit.prevent="nuevo()">
                <p>Area: <input type="text" v-model = "payload.area"  required/></p>
                <button type="submit">Agregar</button>
                </form>

                <form @submit.prevent="nuevo()">
                <p>Movilidad: <input type="text" v-model = "payload.movilidad"  required/></p>
                <button type="submit">Agregar</button>
                </form>

                <form @submit.prevent="nuevo()">
                <p>Placa: <input type="text" v-model = "payload.placa"  required/></p>
                <button type="submit">Agregar</button>
                </form>

                <form @submit.prevent="nuevo()">
                <p>color: <input type="text" v-model = "payload.color"  required/></p>
                <button type="submit">Agregar</button>
                </form>-->

            </div>
  </div>
</div>

<div class="card">
            <div class="card-content">
                <form @submit.prevent="getList()">
                    <h5>Buscar empleado</h5>
                    <p>Nombre empleado: <input type="search" v-model="search" @search="getList()" /></p>
                    <button type="submit" class="waves-effect waves-light btn-small">buscar</button>
                </form>
            </div>
        </div>
    
        <div class="card">
            <div class="card-content">
                <h5>filtro por vehiculo</h5>
                <!-- <p>Filtro por vehiculo: </p> -->
                <div class="input-field ">
                    <select @change="filter('movilidad',$event.target.value)">
                        <option value=" " selected>todos</option> 
                        <!-- <option :value="empleado.movilidad" v-for="empleado in empleado">{{empleado.movilidad}}</option> -->
                        <option value="auto">auto</option>
                        <option value="moto">moto</option> 
                    </select>
                    <!-- <button type="submit" class="waves-effect waves-light btn-small">buscar</button> -->
                      <label>Materialize Select</label> 
                </div>
    
            </div>
        </div>



<div class="card">
            <div class="card-content">
              <table>
                <thead>
                  <tr> 
                    <th>id</th>
                    <th>nombre</th>
                    <th>area</th>
                    <th>movilidad</th>
                    <th>placa</th>
                    <th>color</th>
                  </tr>
                </thead>

                <tbody>
                  <tr v-for="item in items">
                    <td>{{item.id}}</td>
                    <td>{{item.nombre}}</td>
                    <td>{{item.area}}</td>
                    <td>{{item.movilidad}}</td>
                    <td>{{item.placa}}</td>
                    <td>{{item.color}}</td>
                     <th><a class="btn-floating btn-large waves-effect waves-light red"><i class="material-icons" @click="eliminar(item.id)">delete</i></a></th>
                    <th><a class="btn-floating btn-large waves-effect waves-light green"><i class="material-icons" @click="update(item.id)">edit</i></a></th>
                  </tr>
            
                 </tbody>
              </table> 
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
      search: '',
      toFilter: '',
      payload:{
        nombre: null,
        area: null,
        movilidad: null,
        // placa: null,
        // color: null
      }
    }
  },
  methods:{
    filter(movilidad, value) {
            this.toFilter = value === '' ? '' : '&' + movilidad + '=' + value;
            this.getList();
        },
    update(id){
      this.$router.push('/empleado/' + id);
    },
eliminar(id){
  if(confirm("Esta seguro de eliminar?")){
  this.axios({
        method: 'delete',
        url: this.api + '/empleado/' + id,
      })
      
      .then((response)=>{
      this.getList();
       })
      .catch((error)=>{
      console.log(error)
      })
    }      
},
nuevo(){
  this.axios({
    method: 'post',
    url: this.api + '/empleado',
    data: this.payload
  }).
  then((response)=>{
    this.getList();
    console.log(response);
  }).
  catch((error)=>{
    console.log(error);
  })

},

getList(movilidad, value) {

this.axios({
    method: 'get',
    url: this.api + '/empleado?q=' + this.search + this.toFilter
}).
then((response) => {
    this.items = response.data;
}).
catch((error) => {
    console.log(error);
})
}

  },
  components: {
  },
  mounted(){
    this.getList();
        var elems = document.querySelectorAll('select');
        var instances = M.FormSelect.init(elems);
  }
}
</script>
