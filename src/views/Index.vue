<template>
  <div id="Index">
    <div class="encabezado">
      <img class="logo" src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/98/International_Pokémon_logo.svg/640px-International_Pokémon_logo.svg.png" alt="logo">
    </div>
  <div class="form-outline">
      <input type="search" v-model="search"  class="form-control" placeholder="Buscar"  />
  </div>
  <div>
    <PokeDetails :status="status" :info="info" @closeDetails="closeModal"/>
  </div>
  <div class="contenedor-card">
    <div class="row row-cols-1 row-cols-md-5 g-4">
      <div class="col" v-for="(search, index) in filteredPokemons" v-bind:key="index">
        <PokeCard :data="search" v-on:click="openModal(search)"></PokeCard>
      </div>
    </div>
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
      pokemons: {}
    };
  },
  created() {
    let instance = this;
    for(let i=0; i<=99; i++){
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
            comentarios: []
          };
        instance.data.push(pokemon)
          })
          .catch((err) =>{
            console.log(err);
          });
    }
    
  },
  computed:{
    filteredPokemons:function(){
      return this.data.filter((data) =>{
        return data.name.match(this.search);
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
    }
  }
};
</script>

<style>
.encabezado{
  margin-top:45px;
  margin-bottom:100px;
}

.logo{
  margin: auto;
  width: 35%
}

.contenedor-card{
  width: 80%;
  margin: auto;
}

body{
  background-color: #ffffff;
}

.form-outline{
  margin: auto;
  width: 25%;
  margin-bottom: 80px;
}


</style>