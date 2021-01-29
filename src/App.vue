<template>
<Header />
<!-- TODO: Add hourly weather carousel to the top --> 
<FrontPage v-bind:feeds="feeds" /> 
</template>

<script>
import Header from './components/Header'
import FrontPage from './components/FrontPage'
import Parser from 'rss-parser'

export default {
    name: 'app',
    components: {
        Header,
        FrontPage
    },
    data() {
        return {
            feeds: [],
        }
    },
    created() {
        let parser = new Parser();
        const proxyURL = "https://cors-anywhere.herokuapp.com/";
        const urls = ["https://slate.com/feeds/all.rss","https://www.postandcourier.com/search/?t=article&fl=top_story&nsa=eedition&l=10&s=start_time&sd=desc&f=rss"]
        
        urls.forEach(url => {
            parser.parseURL(proxyURL + url)
        .then(feed => {
            console.log(feed)
            this.feeds.push(feed)}
            )
        .catch(err => console.log(err))

        })
        
    }
    
}
</script>

<style scoped>

</style>