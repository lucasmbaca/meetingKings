

<template>
  <div class="container">
    <h1>Cena {{counter + 1}} con el rey godo {{productos[counter].nombre.toLowerCase()}}</h1>
    <h3>Precio: ${{ productos[counter].precio }}</h3>
    <div class="weekened days" v-if="productos[counter].finDeSemana">Solo fines de semana</div>
    <div class="allDays days" v-else>De Lunes a Domingo</div>
    <div class="oferta" v-if="productos[counter].precio < 100">
      <div class="offer-info">
        <div class="oferta-text">ahorra un 10% de descuento: ${{ newPrice }}</div>
        <img src="/oferta.jpg" alt="rey godo en descuento">
      </div>
    </div>
    <div class="image-container">
      <img :src="imagen" alt="Imagen del rey">
      <button @click="nextKing">Siguiente {{counter + 1}}/{{ total }}</button>
    </div>
  </div>
</template>

<script setup>
  import { ref, computed } from "vue";
  import {productos} from "./datos"

  const counter = ref(0);
  const total = productos.length;
  const route = "https://www.html6.es/img/rey_"

  const nextKing = () => {
    counter.value ++
    if (counter.value >= total) {
      counter.value = 0;
    }
  };

  const imagen = computed(()=> {
    return `${route}${productos[counter.value].nombre}.png`
  })

  const newPrice = computed(()=> {
    return Number(productos[counter.value].precio/1.10).toFixed(2)
  });
</script>

<style>
  .container {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    margin: 20px;
    padding: 20px;
    border: 3px solid black;
    border-radius: 5px;
    font-family: Arial, sans-serif;
  }

  h1 {
    font-size: 24px;
    margin-bottom: 10px;
    text-transform: capitalize;
  }

  .oferta {
    display: flex;
    align-items: center;
    margin-top: 20px;
    padding: 10px;
    border-radius: 5px;
  }

  .offer-info {
    display: flex;
    align-items: center;
  }

  .oferta-text {
    font-size: 16px;
    margin-right: 10px;
  }

  .oferta img {
    width: 80px;
    height: auto;
  }

  .image-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 20px;
  }

  button {
    margin-top: 20px;
    padding: 10px 20px;
    background-color: #4CAF50;
    color: white;
    border: none;
    border-radius: 5px;
    font-size: 16px;
    cursor: pointer;
  }

  button:hover {
    background-color: #45a049;
  }
</style>

