<template>
<div class="container">
    <div class="navbar navbar-dark bg-primary mb-2">
        <a href="#" class="navbar-brand">Morning Report</a>
        <div class="navbar-text float-right">{{ today }}</div>
    </div>
</div>
</template>

<script>
export default {
    data() {
        return {
            today: new Date().toLocaleString(),
        }
    }
    
}
</script>

<style scoped>

</style>