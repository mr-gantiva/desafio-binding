<script setup>
import { ref, computed } from 'vue';
import chipOro from './assets/chip.png';
import chipPlata from './assets/chip-plata.png';
import visaImg from './assets/visa.png';
import masterImg from './assets/master.png';


let titulo = ref('');
let numero = ref('');
const fecha = ref('');
const fechaFormateada = ref('');
const propietario = ref('');
let chip = ref('');
let tipoTarjeta = ref('');



let imagenChip = {
  oro: chipOro,
  plata: chipPlata,
}

let imagenTipo = {
  master: masterImg,
  visa: visaImg,
}

// Función para obtener la URL de la imagen del chip
const imageSelector = computed(() => imagenChip[chip.value]);
// Función para obtener la URL de la imagen del tipo de tarjeta
const imageSelectorTipo = computed(() => imagenTipo[tipoTarjeta.value]);

// Función para formatear la fecha
const formatearFecha = () => {
  const [year, month] = fecha.value.split('-');
  fechaFormateada.value = `${month}/${year.slice(-2)}`; // MM/AA
}
</script>

<template>
  <div id="app">
    <form>
      <div>
        <label>Título de la tarjeta: </label>
        <input v-model="titulo" />
      </div>

      <div>
        <!-- <label>Chip SRC: </label>
        <input /> -->
        <label>Chip:</label>
        <select v-model="chip">
          <option value="oro">Oro</option>
          <option value="plata">Plata</option>
        </select>
      </div>

      <div>
        <label>Número: </label>
        <input type="text" v-model="numero" maxlength="12" />
      </div>

      <div>
        <label>Fecha de expiración: </label>
        <input type="month" id="fecha" v-model="fecha" @change="formatearFecha" />
      </div>

      <div>
        <label>Propietario: </label>
        <input type="text" id="propietario" v-model="propietario" />
      </div>

      <div>
        <label>Tipo de tarjeta SRC: </label>
        <select v-model="tipoTarjeta">
          <option value="visa">Visa</option>
          <option value="master">Master</option>
        </select>
      </div>
    </form>

    <div class="carnet">
      <h3>{{ titulo }}</h3>
      <img width="40" :src="imageSelector" alt="" />
      <div>
        <h2>{{ numero }}</h2>
        <span>Fecha Exp: <b>{{ fechaFormateada }}</b></span>
      </div>
      <footer>
        <span>{{ propietario }}</span>
        <img :src="imageSelectorTipo" width="60" />
      </footer>
    </div>
  </div>
</template>

<style scoped>
* {
  margin: 0;
}

body {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100vh;
  font-size: 10px;
  font-family: sans-serif;
}

#app {
  display: flex;
  gap: 40px;
  width: 100%;
}

form {
  padding: 18px;
  border-radius: 20px;
  border: ridge 1px;
  box-shadow: 1px 1px 1px 1px gray;
  font-weight: bold;
  display: flex;
  flex-direction: column;
  gap: 15px;
  justify-content: center;
  background-color: #fff;
}

form div {
  display: grid;
  grid-template-columns: 100px 200px;
  align-items: center;
  gap: 5px;
}

form div label {
  text-align: right;
}

.carnet {
  width: 400px;
  height: 230px;
  background: #1c1a1e;
  color: white;
  border-radius: 20px;
  padding: 20px;
  box-shadow: 0px 0px 10px 2px black;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

h3 {
  font-size: 20px;
}

h2 {
  font-size: 30px;
  letter-spacing: 10px;
  margin-bottom: 15px;
  text-shadow: 0px 0px 1px gold;
  font-family: Times;
}

b {
  font-size: 16px;
}

footer {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  font-weight: bold;
  font-size: 18px;
  text-transform: uppercase;
  font-style: italic;
}
</style>
