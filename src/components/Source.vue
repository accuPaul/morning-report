<template>
<div class="card" style="max-width: 18rem;">
        <div class="card-header bg-light">{{ feed.title }}</div>
        <div class="card-body">
            <ul v-bind:key="article.title" v-for="article in feed.items.slice(position,position+delta)" class="list-group">
            <Article v-bind:article="article" />
            </ul>
        </div>
        <div class="card-footer text-center">
            <button @click="position<10?position=0:position-=10" value="<<">
                <i class="fa fa-caret-left" />
            </button>
            Items {{ position+1 }} - {{ position + 11 }} of {{ feed.items.length }}
            <button @click="position>(limit-delta)?position=limit-delta:position+=10">
                <i class="fa fa-caret-right" />
            </button>
        </div>
</div>
</template>

<script>
import Article from './Article.vue'
export default {
  components: { Article },
    props: ["feed"],
    data() {
        return {
            position: 0,
            limit: this.feed.items.length,
            delta: 10,
        }
    },
    computed: {
        listLimit() {
            return this.limit > this.feed.items.length? this.feed.items : this.feed.items.slice(this.limit)
        }
    }
}
</script>

<style scoped>

</style>