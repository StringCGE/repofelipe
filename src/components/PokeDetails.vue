<template>
  <div class="contenedor-details" v-if="status" :style="{backgroundColor: colorType(info.type)}">
    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-x-lg btn-cerrar" viewBox="0 0 16 16" @click="closeDetails">
      <path fill-rule="evenodd" d="M13.854 2.146a.5.5 0 0 1 0 .708l-11 11a.5.5 0 0 1-.708-.708l11-11a.5.5 0 0 1 .708 0Z"/>
      <path fill-rule="evenodd" d="M2.146 2.146a.5.5 0 0 0 0 .708l11 11a.5.5 0 0 0 .708-.708l-11-11a.5.5 0 0 0-.708 0Z"/>
    </svg>
    <h2>{{info.name}}</h2>
    <div class="items-details">
      <div class="izquierda">
        <img class = "imagen" :src="info.url" />
        <input type="text" class="form-control" name ="comentario" v-model="comentario" placeholder="Escribe un comentario" aria-label="Comentario">
        <label for="comentarios"></label>

      <div class="contenedor-comentarios">
        <ul class="list-group">
          <li class="list-group-item" v-for="lista in info.comentarios" v-bind:key="lista">{{lista}}</li>
        </ul>
      </div>
      </div>
      <div class="derecha">
      <p class="característica">ID: #{{info.id}}</p>
      <p class="característica">Tipo: {{info.type}}</p>
      <p class="característica">Experiencia: {{info.experience}} XP</p>
      <p class="característica">Altura: {{((info.height)*(0.1/1)).toFixed(2)}} m</p>
      <p class="característica">Peso: {{(info.weight)*(1/10)}} kg</p>
      <button type="button" class="btn btn-success boton-comentarios" v-on:click="posicionComentario(); nuevoComentario();" >Añadir comentario</button>
      <button type="button" class="btn btn-danger boton-comentarios" v-on:click="posicionComentario(); limpiarComentarios();">Limpiar Comentarios</button>
      </div>
    </div>
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
      comentario: null
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
    },
    resetInput(){
      this.comentario = '';
    },
    nuevoComentario(){
      if(this.comentario != ''){
        this.$emit('comentario', this.comentario);
        this.resetInput();
      }
    },
    posicionComentario(){
      this.$emit('posicion', this.info.id);
    },
    limpiarComentarios(){
      this.$emit('posicionDelete');
    }
  }
};
</script>

<style scoped>

.contenedor-details{
  position: fixed;
  background-color: #ffff;
  width: 500px;
  left: 50%;
  margin-left: -250px;
  top: 10%;
  border-radius: 15px;
  color: rgb(255, 255, 255);
  box-shadow: 0 5px 20px 0 #2e2e2ebe;
  font-weight: 600;
}


.imagen{
  max-height: 200px;
  max-width: 150px;
  margin: 40px;
  margin-top: 8px;
}

.bi{
  margin: 10px;
  position: absolute;
  right: 3%;
  top: 1%;
  cursor:pointer;
  color: rgb(255, 255, 255);
}

.bi:hover{
  color: rgb(241, 76, 76);
}

h2{
  padding: 20px;
}

.btn{
  margin:20px
}

.items-details{
  display: flex;
}

.derecha{
  width: 90%;
}

.form-control{
  margin: 10px;
}

.contenedor-comentarios{
  max-width: 300px;
  margin-left: 20px;
  margin-bottom: 20px;
  text-align: left;
  background-color: #ffff;
  color: black;
  border-radius: 5px;
  font-weight: 100;
}


</style>