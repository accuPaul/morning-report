<template>
   <div class="container-fluid">
<div v-if="sunError">{{ sunError.message }}</div>
    <div v-else>
        <div class="row justify-content-center mt-1">
            <div class="col-sm-auto" v-if="suntimes">
               <Sundata v-bind:suntimes="suntimes?.results" />
            </div>
            <div v-if="tideError">{{ tideError.message}}</div>
            <div v-else class="col-sm-auto">
               <TideView v-bind:tides="tideData?.predictions" />
            </div>
        </div>
    </div>  
</div> 
</template>

<script>
import axios from 'axios'
import { ref } from 'vue'
import Sundata from '../Sundata.vue';
import TideView from '../TideView.vue';

export default {
  components: { Sundata, TideView },
    async setup() {
        const suntimes = ref(null);
        const sunError = ref(null);
        const tideData = ref(null);
        const tideError = ref(null);
            
        axios.get("https://api.sunrise-sunset.org/json?lat=32.8323&lng=-79.8284&formatted=0", { mode: 'cors'})
            .then(response => {
                suntimes.value = response.data;
                })
            .catch(err => {
                sunError.value = err;
                });
            
           axios.get("https://api.tidesandcurrents.noaa.gov/api/prod/datagetter?product=predictions&application=NOS.COOPS.TAC.WL&date=today&datum=MLLW&station=8665567&time_zone=lst_ldt&units=english&interval=hilo&format=json", { mode: 'cors'})
            .then(response => {
                tideData.value = response.data;
                console.log(tideData.value);
                })
            .catch(err => {
                tideError.value = err;
                });
             
        return { suntimes, sunError, tideData, tideError }
    },
    
}
</script>

<style scoped>

</style>