<template>
    <div class="container-fluid overflow-hidden"
    v-if="foundMovies != null">
        <h3 class="pt-4" v-if="foundMovies.length > 0">Film</h3>
            <vue-horizontal>
                <template v-if="foundMovies.length > 3"
                    v-slot:btn-next>
                    <div class="replaced-btn right">
                        <div><i class="fas fa-angle-right"></i></div>
                    </div>
                    </template>
                    <template v-slot:btn-prev>
                    <div class="replaced-btn left">
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
@import '../assets/style/variables.scss';

h3 {
    color: $secondaryText;
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
    font-size: 50px;
    line-height: 1;
    color: $secondaryText;
    padding: 0 20px;

}


</style>