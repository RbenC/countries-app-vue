<template>
    <div class="paises paises__contenedor">
        <div class="paises__grid">
            <div v-for="country in countries" :key="country.id">
                <CountryItem :country="country"/>
            </div>
        </div>
    </div>
</template>

<script setup>
import { defineProps, toRefs } from 'vue'; 
import CountryItem  from '../components/CountryItem'



const props = defineProps({
    countries: {
        type: Array,
        default: () => [],
    }
});
const { countries }   = toRefs(props); 


</script>
        

<style>
    
</style>