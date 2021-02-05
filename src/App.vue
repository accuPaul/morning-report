<template>
<Header />
<div v-if="error">{{ error }}</div>
<Suspense>
    <template #default>
        <Forecast />
    </template>
    <template #fallback>
        <div class="container">
            <i class="fa fa-spinner">Loading forecast data...</i>
        </div>
    </template>
</Suspense>
<FrontPage v-bind:feeds="feeds" /> 
</template>

<script>
import Header from './components/Header'
import FrontPage from './components/FrontPage'
import Forecast from './components/Forecast'
import Parser from 'rss-parser'
import { onErrorCaptured, ref } from 'vue'

export default {
    name: 'app',
    setup() {
        const error = ref(null);

        onErrorCaptured(e => error.value = e);
        return { error }
    },
    components: {
        Header,
        FrontPage,
        Forecast
    },
    data() {
        return {
            feeds: [],
        }
    },
    created() {
        let parser = new Parser();
        const proxyURL = "https://cors-anywhere.herokuapp.com/";
        const urls = ["https://slate.com/feeds/all.rss","https://www.postandcourier.com/search/?t=article&fl=top_story&nsa=eedition&l=100&s=start_time&sd=desc&f=rss"]
        
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