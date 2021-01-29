<template>
    <div class="list-group-item flex-column align-items-start mb-2">
            <a :href="article.link"><h5>{{article.title}}</h5></a>
            <p class="mb-1">{{ article.contentSnippet}} </p>
            <small>{{article.pubDate}}</small>
        </div>
</template>

<script>
export default {
    props: ["article"]
    
}
</script>

<style scoped>

</style>