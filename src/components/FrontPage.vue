<template>
<div class="container">
    <div class="card" v-bind:key="feed.title" v-for="feed in feeds">
        <div class="card-header">{{ feed.title }}</div>
        <div class="card-body">
            <div v-bind:key="article.title" v-for="article in feed.items" class="list-group">
            <Article v-bind:article="article" />
            </div>
        </div>
    </div>
</div>
</template>

<script>
import Article from './Article.vue'
export default {
  components: { Article },
    props: ["feeds"]
}
</script>

<style scoped>

</style>