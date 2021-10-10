<template>
    <div class="container-fluid overflow-hidden"
    v-if="foundShows != null">
        <h3 class="pt-4" 
        v-if="foundShows.length > 0">
            Serie TV
            <span v-if="foundShows == trends">
                - Trend della settimana
            </span>
        </h3>
        <h2 class="my-5"
        v-else>
            Nessuna serie trovata
        </h2>
        <vue-horizontal>
            <template v-if="foundShows.length > 3" 
                v-slot:btn-next>
                    <div class="replaced-btn right"
                    v-if="foundShows.length > 0">
                        <div><i class="fas fa-angle-right"></i></div>
                    </div>
                    </template>
                    <template v-slot:btn-prev>
                    <div class="replaced-btn left"
                    v-if="foundShows.length > 0">
                        <div><i class="fas fa-angle-left"></i></div>
                    </div>
                </template>
            <ShowCard class="item mx-2"
            v-for="(sh, index) in foundShows" 
            :key="index" 
            :show="sh"/>
        </vue-horizontal>
        
    </div>
</template>

<script>
import ShowCard from '../components/ShowCard';
import axios from 'axios';
import VueHorizontal from 'vue-horizontal';

export default {
    name: 'Shows',
    components: {
        ShowCard,
        VueHorizontal
    },
    props: ['srcTitle'],
    data() {
        return {
            foundShows: [],
            trends: []
        }
    },
    created(){
    axios
        .get("https://api.themoviedb.org/3/trending/tv/week",{
            params:{
                api_key: 'c0af7194607876d6036970e4504abc6d',
                language: 'it-IT'
            }
        }
        )
        .then(
            (resp)=>{
                    this.foundShows = resp.data.results;
                    this.trends = resp.data.results;
                }
        )
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
                this.foundShows = this.trends;
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
    font-size: 50px;
    line-height: 1;
    color: $secondaryText;
    padding: 0 20px;

}
</style>