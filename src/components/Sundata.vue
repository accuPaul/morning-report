<template>
<div class="card">
    <div class="card-header">
        Sun Data
    </div>
    <div class="card-body">
        <div class="card-text float-left">
            <i class="fa fa-arrow-up fa-sm" />Sunrise: {{ riseTime }}
        <br />
        <span class="float-right">Sunset: {{ setTime }} <i class="fa fa-arrow-down  fa-sm" /></span>
        <br />
        Length of daylight {{ sunHours }}:{{ sunMinutes }}
        </div>
    </div>
</div>
    
</template>

<script>
export default {
    props: ["suntimes"],
    data() {
        return {
            sunHours: Math.round(this.suntimes.day_length/3600).toString(),
            sunMinutes: Math.round((this.suntimes.day_length%3600)/60).toString(),
            riseTime: new Date(this.suntimes.sunrise).toLocaleTimeString(),
            setTime: new Date(this.suntimes.sunset).toLocaleTimeString(),
            }
    }
}

</script>

<style scoped>

</style>