<template>
    <div class="card" :style="replacePath()">
        <div class="details w-100 h-100 d-flex flex-column">
            <h2 class="fw-bolder">
                {{movie.title}}
            </h2>
            <div v-if="movie.title.toLowerCase() != movie.original_title.toLowerCase()">
                <div class="fw-bold">
                    Titolo originale:
                </div> 
                <h5>{{movie.original_title}}</h5>
            </div>
            <div class="py-2">
                <span class="fw-bold pe-2">Lingua:</span>  
                <lang-flag 
                :iso="`${movie.original_language}`" 
                :class="{unaviable_flag : aviableFlags.includes(this.movie.original_language) == false}"/>
            </div>
            <div>
                <span class="fw-bold pe-2">Voto:</span>
                <i class="fas fa-star" 
                v-for="(n, index) in rating" 
                :key="index"></i>
                <i class="far fa-star" 
                v-for="(n, index) in (5 - rating)" 
                :key="index + 'empty'"></i>
            </div>
            <p v-if="movie.overview" class="mt-2">
                <span class="fw-bold">Overview:</span> 
                "{{movie.overview}}"
            </p>
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
                return `background-image: url(${require('../assets/images/netflix.jpg')})`;
            } else {
                return `background-image: url(https://image.tmdb.org/t/p/original${this.movie.poster_path})`;
            }
        }
    }
}
</script>

<style scoped lang="scss">
@import '../assets/style/variables.scss';

.card {
    display: inline-block;
    width: 300px;
    height: 450px;
    background-size: cover;
    background-position: center;
    .details {
        opacity: 0;
        padding: 2.5rem .625rem .625rem;
        background-color: rgba(0, 0, 0, 0.9);
        box-shadow: 0 0 0 2px rgba(0,0,0,0.9);
        .fw-bold {
            color: $secondaryText;
        }
        h2 {
            
            margin-bottom: 20px;
        }
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
        p {
            height: 100%;
            overflow: auto;
            scrollbar-width: none;
            -ms-overflow-style: none;
        }
        p::-webkit-scrollbar {
            display: none;
        }
    }
    .details:hover {
        opacity: 1;
    }
}

</style>