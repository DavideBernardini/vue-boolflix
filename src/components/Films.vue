<template>
    <div class="container-fluid overflow-hidden"
    v-if="foundMovies != null">
        <h2 h2 v-if="foundMovies.length > 0">Film</h2>
        <div class="row row-cols-5 flex-nowrap overflow-auto">
            <FilmCard class="col mb-3 ms-3" 
            v-for="(mv, index) in foundMovies" 
            :key="index" :movie="mv"/>
        </div>
        
    </div>
</template>

<script>
import FilmCard from '../components/FilmCard';
import axios from 'axios';

export default {
    name: 'Films',
    components: {
        FilmCard,
    },
    props: ['srcTitle'],
    data() {
        return {
            foundMovies: []
        }
    },
    watch: {
        srcTitle: function() {
            if (this.srcTitle != '') {
                axios
                .get('https://api.themoviedb.org/3/search/movie', {
                    params: {
                    api_key: 'c0af7194607876d6036970e4504abc6d',
                    query: this.srcTitle,
                    language: 'it-IT'
                    }
                })
                .then( (response) => {
                    this.foundMovies = response.data.results;
                });
            } else {
                this.foundMovies = null;
            }
        }
    }
}
</script>

<style scoped lang="scss">

</style>