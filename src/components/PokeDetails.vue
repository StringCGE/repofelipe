<template>
  <div class="contenedor-details" v-if="status" :style="{backgroundColor: colorType(info.type)}">
    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-x-lg btn-cerrar" viewBox="0 0 16 16" @click="closeDetails">
      <path fill-rule="evenodd" d="M13.854 2.146a.5.5 0 0 1 0 .708l-11 11a.5.5 0 0 1-.708-.708l11-11a.5.5 0 0 1 .708 0Z"/>
      <path fill-rule="evenodd" d="M2.146 2.146a.5.5 0 0 0 0 .708l11 11a.5.5 0 0 0 .708-.708l-11-11a.5.5 0 0 0-.708 0Z"/>
    </svg>
    <h2>{{info.name}}</h2>
    <img class = "imagen" :src="info.url" />
    <p class="característica">ID: #{{info.id}}</p>
    <p class="característica">Tipo: {{info.type}}</p>
    <p class="característica">Experiencia: {{info.experience}} XP</p>
    <p class="característica">Altura: {{((info.height)*(0.1/1)).toFixed(2)}} m</p>
    <p class="característica">Peso: {{(info.weight)*(1/10)}} kg</p>
</div>
</template>

<script>

export default {
  props: {
    info: null,
    status: Boolean
  },
  data() {
    return {
    };
  },
  methods:{
    closeDetails(){
      this.$emit('closeDetails', false);
    },
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
  }
};
</script>

<style scoped>

.contenedor-details{
  position: fixed;
  background-color: #ffff;
  width: 450px;
  left: 50%;
  margin-left: -250px;
  top: 20%;
  border-radius: 15px;
  color: rgb(255, 255, 255);
  box-shadow: 0 5px 20px 0 #2e2e2ebe;
  font-weight: 600;
}

.imagen{
  height: 200px;
}

.bi{
  margin: 10px;
  position: absolute;
  right: 3%;
  top: 1%;
  cursor:pointer;
  color: rgb(201, 12, 12);
}

h2{
  padding: 20px;
}

</style>