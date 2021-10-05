<template>
    <div>
        <FilmCard/>
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
    props: ['searchTitle'],
    created() {
        axios
        .get('https://api.themoviedb.org/3/search/movie', {
            params: {
            api_key: 'c0af7194607876d6036970e4504abc6d',
            query: 'Aldo, Giovanni e Giacomo',
            language: 'it-IT'
            }
        })
        .then(function (response) {
            console.log(response.data);
        });  
    }
}
</script>

<style scoped lang="scss">

</style>