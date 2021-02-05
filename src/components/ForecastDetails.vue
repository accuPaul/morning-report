<template>
<div class="card" v-bind:class="forecast.hasPrecipitation?'border-danger':'border-success'">
    <div class="card-header">{{ forecastTime }}</div>
    <img v-bind:src="getIcon" class="card-img-top" />
    <div class="card-body">
        <div class="card-title">{{forecast.IconPhrase}}</div>
        <div class="card-text">{{forecast.Temperature.Value}}</div>
    </div>
    <div class="list-group-flush">
        <div class="list-group-item">
           Wind {{ windRange }} 
            </div>
        <div class="list-group-item">POP: {{ forecast.PrecipitationProbability }}%</div>
    </div>
</div>
    
</template>

<script>
export default {
    props: ["forecast"],
    data() {
        return {
            forecastTime: new Date(this.forecast.DateTime).toLocaleTimeString(),
            windRange: Math.round(this.forecast.Wind.Speed.Value).toString()+" - "
                +Math.round(this.forecast.WindGust.Speed.Value),
                getIcon: "https://picklewx.netlify.app/icons/"+
                (this.forecast.WeatherIcon.toString().length==1?
                "0":"") + this.forecast.WeatherIcon.toString()+"-s.png",
            }
    }
}

</script>

<style scoped>

</style>