<template>
<div class="card">
    <div class="card-header">
        Today's Tides
    </div>
    <div class="card-body">
    <div class="card-text" v-bind:key="tide.t" v-for="tide in tides">
        <p class="mr-1 ml-1 mb-1">
            <span class="float-left">{{ tide.type=="H"?"High":"Low" }}...</span>
            <span class="float-right">{{ formatTime(tide.t) }} ({{ formatHeight(tide.v) }}') </span>
        </p>
    </div>
    </div>
    
</div>
    
</template>

<script>
export default {
    props: ["tides"],
    methods:  {
        formatTime(tideTime) {
            return tideTime.split(" ")[1]
        },
        formatHeight(height) {
            return (Math.round(height*10)/10).toString()
        },
    }
}

</script>

<style scoped>

</style>