<template>
    <div>
        <FilmCard v-for="(mv, index) in foundMovies" :key="index" :movie="mv"/>
    </div>
</template>

<script>
import FilmCard from '../components/FilmCard';
import axios from 'axios';

export default {
    name: 'Films',
    components: {
        FilmCard
    },
    props: ['srcTitle'],
    data() {
        return {
            foundMovies: []
        }
    },
    created() {
        axios
        .get('https://api.themoviedb.org/3/search/movie', {
            params: {
            api_key: 'c0af7194607876d6036970e4504abc6d',
            query: 'ritorno al futuro',
            language: 'it-IT'
            }
        })
        .then( (response) => {
            this.foundMovies = response.data.results;
        });  
    }
}
</script>

<style scoped lang="scss">

</style>