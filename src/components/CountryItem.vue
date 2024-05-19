<template>
    <div class="pais">
        <img :src="country.flags.png" :alt="country.name.commom" class="pais__imagen"/>
        <div class="pais__contenido">
            <p class="pais__nombre" >{{ country.name.common }} </p>
            <p class="pais__capital"> <span>Capital</span> {{ country.capital }}</p>
            <p class="pais__area"><span>Km</span> {{ country.area }} <span>Pob. {{ country.population }}</span> </p>
        </div>              
    </div>
</template>

<script setup>

import { defineProps,  toRefs }  from 'vue'; 




const props = defineProps({
    country: {
        type: {},
    }
}); 

const { country } = toRefs(props); 
    
</script>

<style>
    
</style>