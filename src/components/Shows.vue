<template>
    <div v-if="foundShows != null">
        <h2 v-if="foundShows.length > 0">Serie TV</h2>
        <ShowCard v-for="(sh, index) in foundShows" 
        :key="index" :show="sh"/>
    </div>
</template>

<script>
import ShowCard from '../components/ShowCard';
import axios from 'axios';

export default {
    name: 'Shows',
    components: {
        ShowCard
    },
    props: ['srcTitle'],
    data() {
        return {
            foundShows: []
        }
    },
    watch: {
        srcTitle: function() {
            if (this.srcTitle != '') {
                axios
                .get('https://api.themoviedb.org/3/search/tv', {
                    params: {
                    api_key: 'c0af7194607876d6036970e4504abc6d',
                    query: this.srcTitle,
                    language: 'it-IT'
                    }
                })
                .then( (response) => {
                    this.foundShows = response.data.results;
                });
            } else {
                this.foundShows = null;
            }
        }
    }
}
</script>

<style scoped lang="scss">

</style>