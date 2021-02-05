<template>
<div class="container">
<div v-if="error">{{ error.message }}</div>
    <div v-else>
        <div class="row">
        <div class="card-group" v-bind:key="forecast.EpochDateTime" v-for="forecast in forecasts">
            <div class="col container-fluid mt-1">
               <ForecastDetails v-bind:forecast="forecast" />
            </div>
        </div>
        </div>
    </div>  
</div>
</template>

<script>
import axios from 'axios'
import { ref } from 'vue'
import ForecastDetails from './ForecastDetails'

export default {
    components: { ForecastDetails },
    async setup() {
        const forecasts = ref(null);
        const error = ref(null);
        //const proxyUrl = process.env.VUE_APP_PROXY;

            
        axios.get(`https://${process.env.VUE_APP_HOST}/forecasts/v1/hourly/12hour/7-340578_1_AL?details=true&apikey=${process.env.VUE_APP_KEY}`, { mode: 'cors'})
            .then(response => {
                forecasts.value = response.data;
                console.log(forecasts.value)
                })
            .catch(err => {
                error.value = err;
                });
            
        return { forecasts, error}
    }
}
</script>

<style scoped>

</style>