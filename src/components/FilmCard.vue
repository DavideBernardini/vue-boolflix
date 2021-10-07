<template>
    <div class="card" :style="replacePath()">
        <h2>
            Title: {{movie.title}}
        </h2>
        <h3 v-if="movie.title.toLowerCase() != movie.original_title.toLowerCase()">
            Original title: {{movie.original_title}}
        </h3>
        <div>
            <span>Lang:  </span>  
            <lang-flag 
            :iso="`${movie.original_language}`" 
            :class="{unaviable_flag : aviableFlags.includes(this.movie.original_language) == false}"/>
        </div>
        <div>
            <i class="fas fa-star" 
            v-for="(n, index) in rating" 
            :key="index"></i>
            <i class="far fa-star" 
            v-for="(n, index) in (5 - rating)" 
            :key="index + 'empty'"></i>
        </div>
    </div>
</template>

<script>
import LangFlag from 'vue-lang-code-flags'

export default {
    name: 'FilmCard',
    components: {
        LangFlag
    },
    props: ['movie'],
    data() {
        return {
            aviableFlags: [
                'en',
                'zh',
                'hi',
                'es',
                'ar',
                'fr',
                'ms',
                'ru',
                'bn',
                'pt',
                'de',
                'ja',
                'fa',
                'sw',
                'jv',
                'te',
                'tr',
                'ko',
                'mr',
                'ta',
                'vi',
                'it',
                'ha',
                'th',
                ]
        }
    },
    computed: {
        rating() {
            return Math.ceil(this.movie.vote_average / 2);
        }
    },
    methods: {
        replacePath() {
            if (this.movie.poster_path == null) {
                return 'background-image: url(../assets/images/Netflix.jpg)'
            } else {
                return `background-image: url(https://image.tmdb.org/t/p/original${this.movie.poster_path})`;
            }
        }
    }
}
</script>

<style scoped lang="scss">
.card {
    display: inline-block;
    width: 300px;
    height: 450px;
    background-size: cover;
    background-position: center;
    span {
        vertical-align: middle;
        background-size: cover !important;
        width: 20px !important;
    }
    .unaviable_flag {
        background-image: url(https://upload.wikimedia.org/wikipedia/commons/3/35/Orange_question_mark.svg) !important;
        width: 16px !important;
    }
    i {
        color: rgb(245, 210, 10);
    }
}
</style>