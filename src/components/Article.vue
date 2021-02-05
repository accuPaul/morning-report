<template>
    <li class="flex-column align-items-start ml-1 mb-1">
            <a :href="article.link" :hover="article.contentSnippet" data-toggle="tooltip" :title="article.contentSnippet">{{article.title}}</a>
            <p><small>{{article.pubDate}}</small></p>
        </li>
</template>

<script>
export default {
    props: ["article"]
    
}
</script>

<style scoped>

</style>