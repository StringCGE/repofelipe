<template>
  <div class="container">
    <div class="poke-card" :src="data.url" :style="{backgroundColor: colorType(data.type)}">
      <img class = "imagen" :src="data.url" :style="{backgroundColor: colorType(data.type)}">
      <div class="poke-data" :src="data.url" :style="{backgroundColor: colorType(data.type)}">
        <h5 class="poke-name">
          {{data.name}}
        </h5>
      </div>
    </div>
  </div>
    
</template>

<script>
export default {
  name: 'PokeCard',
  components:{ 
  },
  props:{
    data: null
  },
  data(){
    return{
      
    }
  },
  methods:{
    colorType(type){
      switch(type){
        case 'grass': return '#48d0b1';
        case 'fire': return '#fb6c6c';
        case 'water': return '#76bdfe';
        case 'bug': return '#f7786b';
        case 'normal': return '#b1736c';
        case 'electric': return '#faa307';
        case 'poison': return '#46B00C';
        case 'ground': return '#532A5E';
        case 'fighting': return '#00364F';
        case 'psychic': return '#7D207B';
        case 'rock': return '#3D3D3D';
        case 'fairy': return '#C552B3';
        case 'ghost': return '#5C5C84';
        case 'dragon': return '#750F13';
        case 'ice': return '#89b0ae';
        case 'dark': return '#292A33';
        case 'steel': return '#7D95B8';
        case 'flying': return '#7DF8AA';
      }
    }
  },
}
</script>

<style scoped>

.poke-card {
  width: 180px;
  height: 200px;
  margin: 15px;
  border-radius: 20px;
  cursor: pointer;
  font-family: 'Roboto';
}

.poke-card:hover {
  box-shadow: 0 1px 20px 0 #e0e0e0b9;
  transition: 0.2s;
}

.poke-data {
  padding: 2px 16px;
  border-radius: 20px;

}

.imagen{
  margin: 40px;
  max-width: 90px;
  max-height: 90px;
  border-radius: 20px;
}

.poke-name{
  color: #ffff;
  font-weight: 500;
}


</style>