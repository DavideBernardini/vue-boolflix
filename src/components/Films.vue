<template>
    <div class="container-fluid overflow-hidden"
    v-if="foundMovies != null">
        <h3 class="pt-4" 
        v-if="foundMovies.length > 0">
            Film
            <span v-if="foundMovies == trends">
                - Trend della settimana
            </span>
        </h3>
        <h2 class="my-5 pt-4"
        v-else>
            Nessuna film trovato
        </h2>
        <vue-horizontal>
            <template v-if="foundMovies.length > 3"
                v-slot:btn-next>
                <div class="replaced-btn right"
                v-if="foundMovies.length > 0">
                    <div><i class="fas fa-angle-right"></i></div>
                </div>
                </template>
                <template v-slot:btn-prev>
                <div class="replaced-btn left"
                v-if="foundMovies.length > 0">
                    <div><i class="fas fa-angle-left"></i></div>
                </div>
            </template>
            <FilmCard class="item mx-2" 
            v-for="(mv, index) in foundMovies" 
            :key="index" :movie="mv"/>
        </vue-horizontal>
    </div>
</template>

<script>
import FilmCard from '../components/FilmCard';
import axios from 'axios';
import VueHorizontal from 'vue-horizontal';

export default {
    name: 'Films',
    components: {
        FilmCard,
        VueHorizontal
    },
    props: ['srcTitle'],
    data() {
        return {
            foundMovies: [],
            trends: []
        }
    },
    created(){
    axios
        .get("https://api.themoviedb.org/3/trending/movie/week",{
            params:{
                api_key: 'c0af7194607876d6036970e4504abc6d',
                language: 'it-IT'
            }
        }
        )
        .then(
            (resp)=>{
                    this.foundMovies = resp.data.results;
                    this.trends = resp.data.results;
                }
        )
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
                this.foundMovies = this.trends;
            }
        }
    }
}
</script>

<style scoped lang="scss">
@import '../assets/style/variables.scss';

h3 {
    color: $secondaryText;
    span {
        font-size: 1.5rem;
    }
}
h2 {
    color: $secondaryText;
    display: inline-block;
}
.replaced-btn {
    height: 100%;
    display: flex;
    align-items: center;
}
.replaced-btn.left {
    background: linear-gradient(to left, #ffffff00, black);
    transform: translateX(50%);
}
.replaced-btn.right {
    background: linear-gradient(to right, #ffffff00, black);
    transform: translateX(-50%);
}
.replaced-btn > div {
    font-size: 3.125rem;
    line-height: 1;
    color: $secondaryText;
    padding: 0 1.25rem;

}
</style>