<template>
<div class="container mt-2">
    <div class="row">
        <div class="col-sm-6" v-bind:key="feed.title" v-for="feed in feeds">
            <Source v-bind:feed="feed" />
        </div>
    </div>
</div>
</template>

<script>
import Source from '../Source.vue'
export default {
  components: { Source },
    props: ["feeds"],
}
</script>

<style scoped>

</style>