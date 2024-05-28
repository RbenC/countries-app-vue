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
      <div class="buttons" >
        <button
          :disabled="page <= 1"  
          class="btn"         
          @click="changePage(page - 1)" >
          Prv
        </button>
        <button         
          :disabled="page >= Math.round(totalItems / itemsPerPage)"      
          class="btn"         
          @click="changePage(page + 1)" >
          Nxt
        </button>
      </div>
  
  
      <!-- <CountryList 
        :countries="filteredCountries.length > 0 ? filteredCountries : countries "
      /> -->
      <CountryList 
        :countries="paginetedCountries"
      />
  
  
      
    </div>
    <!-- <div v-for="country in countries" :key="country.id"> {{ country.name.common }}</div> -->
  </template>
  
  
  
  <script setup>
  import '@/assets/css/normalize.css'
  import '@/assets/css/app.css'
  
  import { onMounted,ref,watch } from 'vue';
  import PageHeader from '@/components/PageHeader.vue';
  import CountryList  from '@/components/CountryList.vue';
  import axiosClient from '@/utils/axios'; 
  import Swal from 'sweetalert2';
  
  
  const countries = ref([]);
  const search = ref("");
  const filteredCountries =ref([]);
  
  const page = ref(1);
  const itemsPerPage = ref(12);
  const paginetedCountries = ref([]); 
  const totalItems = ref(0); 
  
  
  const fetchCountries = async() => {
    try {
      const { data }  = await axiosClient.get("/all");     
      countries.value=data;  
      totalItems.value = countries.value.length;   
    } catch (error) {
      Swal.fire("Error en la carga de datos");
    }
  }
  
  onMounted(() => {
    fetchCountries();   
    
  })
  
  
  const filterCountries = () => {
    filteredCountries.value = countries.value.filter((country)=> country.name.common.toLowerCase().includes(search.value.toLowerCase()));  
  }
  
  const slicedCountries = (currentCountries) => {
    const start = (page.value - 1) * itemsPerPage.value;
    const end = page.value * itemsPerPage.value; 
    paginetedCountries.value = currentCountries.slice(start, end); 
  }
  
  const changePage = (newPage) => {
    page.value = newPage
  }
  
  watch([countries, page, filteredCountries], () => {
    slicedCountries(
      filteredCountries.value.length <= 0  && search.value === ""
      ? countries.value 
      : filteredCountries.value
    );
  });
  
  
  
  
  </script>
  
  
  <style>
    
  </style>