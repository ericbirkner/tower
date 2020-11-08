<template>
  <div class="row">
    <div class="col-12 fixed-top buscador shadow pb-2 pt-2">
      <h1>Bienvenido al buscador de profesionales Tower</h1>
      
      <div class="input-group">
        <input type="text" class="form-control" placeholder="Buscar profesional por nombre" v-model="nombre" @keypress="buscar()">
        <div class="input-group-append">
          <button class="btn btn-secondary" type="button" @click="buscar()">
            <i class="fa fa-search"></i>
          </button>
        </div>
      </div>

    </div>
  
    <div class="col-12 text-center resultados">

      <div class="row mt-4">

        <div class="col-sm-12 col-md-4 col-lg-4" v-for="persona in personas" :key="persona.id">
         
          <Card :datos=persona></Card>

        </div>

      </div>

      <div class="spinner-border mt-4" style="width: 3rem; height: 3rem;" role="status" v-if="loading">
        <span class="sr-only">Cargando...</span>
      </div>

    </div>
    
    <div class="col-12 mb-4">
      <button class="btn btn-primary ver-mas" @click="buscar()" v-if="offset > 0">Ver más</button>
    </div>

   
  
  </div>
</template>

<script>
import axios from 'axios';
import Card from '@/components/Card.vue'
export default {
  name: 'Buscador',
  components: {
    Card
  },
  props: {
    msg: String
  },
  data() {
    return {
      nombre:'',
      personas:[],
      loading: false,
      offset:0,
      size:24
    };
  },
  methods:{
    buscar(){

      if(this.nombre.length===0){
        this.offset= 0;
        this.personas = [];
        this.loading=false;
      }
      if(this.nombre.length>2){
        this.loading=true;
        let params = {
          "name": {
              "term": this.nombre
          }
        };
        let ref =this;
        axios.post('https://search.torre.co/people/_search/?size='+ref.size+'&lang=es&aggregate=false&offset='+ref.offset, params, {
          headers: {
              'content-type': 'application/json',
          },
        })
        .then(function (response) {
          console.log(response);
          ref.offset= ref.offset + ref.size;
          ref.personas = ref.personas.concat(response.data.results);
          ref.loading=false;
          
        })
        .catch(function (error) {
          console.log(error);
        });
      }
      
    }
  },
  created: function() {
    
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.ver-mas{
  font-size: 20px;
  font-weight: bold;
}

.buscador{
  background: white;
}

.resultados{
  padding-top: 100px;
}

@media only screen and (max-width: 600px) {
  h1 {
    font-size: 20px;
  }
}
</style>
