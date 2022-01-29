<template>
  <div id="Index">
    <div class="encabezado">
      <img class="logo" src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/98/International_Pokémon_logo.svg/640px-International_Pokémon_logo.svg.png" alt="logo">
      <div class="integrantes">
        <p>Guillén Mirabá José</p>
        <p>Guzmán Bedor Otto</p>
        <p>Jaramillo Ramirez Valeria</p>
        <p>Rodriguez Merchan Darwin</p>
      </div>
    </div>
  <div class="form-outline">
      <input type="search" v-model="search"  class="form-control" placeholder="Buscar"  />
  </div>
  <div>
    <PokeDetails :status="status" :info="info" @closeDetails="closeModal" @comentario="comentario" @posicion="posicionComentario" @posicionDelete="posicionEliminar" />
  </div>
  <div class="contenedor-card">
    <div class="row row-cols-1 row-cols-md-5 g-4">
      <div class="col" v-for="(data, index) in filteredPokemons" v-bind:key="index">
        <PokeCard :data="data" v-on:click="openModal(data)"></PokeCard>
      </div>
    </div>
  </div>
  <div class="contenedor-paginacion">
      <nav aria-label="Page navigation example">
        <ul class="pagination">
          <li v-for="pagina in totalPaginas()" v-bind:key="pagina" v-on:click="getDataPagina(pagina)" class="page-item"><a class="page-link" href="#">{{pagina}}</a></li>
        </ul>
      </nav>
      </div>
  </div>
</template>

<script>
import axios from 'axios';
import PokeCard from '../components/PokeCard.vue';
import PokeDetails from '../components/PokeDetails.vue'

export default {
  name: "Index",
  components:{
     PokeCard, 
     PokeDetails
  },
  data() {
    return {
      data: [],
      search: '',
      status: false,
      info:[],
      posicion: null,
      nombrePokemon: null,
      elementosPorPagina: 60,
      datosPaginados: []
    };
  },
  mounted(){
  },
  created() {
    let instance = this;
    for(let i=0; i<=599; i++){
        axios.get(`https://pokeapi.co/api/v2/pokemon/${i+1}`)
        .then((response) => {
          let pokemon={
            id: response.data.order,
            name : response.data.name,
            url: response.data.sprites.other.dream_world.front_default,
            type: response.data.types[0].type.name,
            experience: response.data.base_experience,
            height: response.data.height,
            weight: response.data.weight,
            comentarios: [],
            paginaActual: 1
          };
        instance.data.push(pokemon);
        this.getDataPagina(1);
          })
          .catch((err) =>{
            console.log(err);
          });
    }
  },
  computed:{
    filteredPokemons:function(){
      return this.datosPaginados.filter((datosPaginados) =>{
          return datosPaginados.name.match(this.search);
      });
    }
  },
  methods:{
    openModal(search){
      this.status = true;
      this.info = search;
    },
    closeModal(value){
      this.status = value;
    },
    comentario(value){
      for(let i=0; i<600; i++){
        if(this.data[i].id == this.posicion){
          this.data[i].comentarios.push(value);
          this.nombrePokemon = this.data[i].name;
          let comentarioLocal = {
            nombre: this.nombrePokemon,
            comment: value
          }
          localStorage.setItem('comentario', JSON.stringify(comentarioLocal));
        }
      }
    },
    posicionComentario(value){
      this.posicion = value;
      console.log(this.posicion);
    },
    posicionEliminar(){
      for(let i=0; i<600; i++){
        if(this.data[i].id == this.posicion){
          this.data[i].comentarios = [];
        }
      }
    },
    totalPaginas(){
      return Math.ceil(600 / this.elementosPorPagina)
    },
    getDataPagina(noPagina){
      this.datosPaginados = [];
      let ini = (noPagina * this.elementosPorPagina) - this.elementosPorPagina;
      let fin = (noPagina * this.elementosPorPagina);

      this.datosPaginados = this.data.slice(ini, fin);
    }
  }
};
</script>

<style>
.encabezado{
  margin-top:45px;
  margin-bottom:100px;
}

.integrantes{
  font-family: 'Roboto';
  color: rgb(255, 255, 255);
  text-align: left;
  position: absolute;
  top: 20px;
  left: 10px;
  font-size: 12px;
}

.logo{
  margin: auto;
  width: 35%
}

.contenedor-card{
  width: 80%;
  margin-left: 105px;
}

body{
  background-color: #1969c4dc;
}

.form-outline{
  margin: auto;
  width: 25%;
  margin-bottom: 80px;
}

.contenedor-paginacion{
  position:relative;
  margin-left: 500px;
  margin-top: 50px
}


</style>