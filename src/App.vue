<template>
  <PageHeader />

  <div class="busqueda busqueda__contenedor">
    <div class="busqueda__pais">
      <input       
        type="text"
        class="busqueda__texto"
        placeholder="Search by country name"
        v-model="search"
        @input="filterCountries"
      >
    </div>

    <CountryList :countries="filteredCountries.length > 0 ? filteredCountries : countries "/>
    
  </div>
  <!-- <div v-for="country in countries" :key="country.id"> {{ country.name.common }}</div> -->
</template>



<script setup>
import './assets/css/normalize.css'
import './assets/css/app.css'

import { onMounted,ref } from 'vue';
import PageHeader from './components/PageHeader.vue'
import CountryList  from './components/CountryList.vue'
import axiosClient from './utils/axios'; 
import Swal from 'sweetalert2'



const countries = ref([]);
const search = ref("");
const filteredCountries =ref([]);





const fetchCountries = async() => {

  try {
    /* usando axios*/
    const { data }  = await axiosClient.get("/all");     
    countries.value=data; 
    /* usando axios*/

    /* Usando fetch*/
        // fetch('https://restcountries.com/v3.1/all')
        // .then(response => response.json())
        // .then(data => countries.value=data);
    /* Usando fetch*/
    

  } catch (error) {
    Swal.fire("Error en la carga de datos");
  }
}
 
onMounted(() => {
  fetchCountries(); 
})



</script>


<style>
  
</style>