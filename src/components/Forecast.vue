<template>
<div class="container-fluid">
<div v-if="error">{{ error.message }}</div>
    <div v-else>
        <div class="row justify-content-center">
            
        <div class="card-group">
           <div class="col col-sm-1 align-self-center" v-show="hour > 0">
                       <button @click="hour>0?hour--:hour"><i class="fa fa-caret-left"></i></button>
           </div>
            <div class="col-sm-auto" v-bind:key="forecast.EpochDateTime" v-for="forecast in forecasts?.slice(hour,hour+numHours)">
               <ForecastDetails v-bind:forecast="forecast" />
            </div>
            <div class="col col-sm-1 align-self-center" v-show="hour < limit">
                <button @click="hour>=limit?hour=limit:hour++"><i class="fa fa-caret-right"></i></button>
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
        const limit = ref(null);
        const hour = ref(null);
        const numHours = ref(null);
        //const proxyUrl = process.env.VUE_APP_PROXY;

            
        axios.get(`https://${process.env.VUE_APP_HOST}/forecasts/v1/hourly/12hour/7-340578_1_AL?details=true&apikey=${process.env.VUE_APP_KEY}`, { mode: 'cors'})
            .then(response => {
                forecasts.value = response.data;
                hour.value = 0;
                numHours.value = 3;
                limit.value = forecasts.value.length - numHours.value;
                })
            .catch(err => {
                error.value = err;
                });
            
        return { forecasts, error, limit, hour, numHours }
    },
}
</script>

<style scoped>

</style>