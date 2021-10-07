<template>
    <div class="card" :style="replacePath()">
        <div class="details w-100 h-100 d-flex flex-column">
            <h2 class="fw-bolder">
                {{show.name}}
            </h2>
            <div v-if="show.name.toLowerCase() != show.original_name.toLowerCase()">
                <div class="fw-bold">
                    Titolo originale:
                </div> 
                <h5>{{show.original_name}}</h5>
            </div>
            <div class="py-2">
                <span class="fw-bold pe-2">Lingua:</span>   
                <lang-flag 
                :iso="`${show.original_language}`" 
                :class="{unaviable_flag : aviableFlags.includes(this.show.original_language) == false}"/>
            </div>
            <div class="pt-2">
                <span class="fw-bold pe-2">Voto:</span>
                <i class="fas fa-star" 
                v-for="(n, index) in rating" 
                :key="index"></i>
                <i class="far fa-star" 
                v-for="(n, index) in (5 - rating)" 
                :key="index + 'empty'"></i>
            </div>
            <p v-if="show.overview" class="mt-2">
                <span class="fw-bold">Overview:</span> 
                "{{show.overview}}"
            </p>
        </div>
        
    </div>
</template>

<script>
import LangFlag from 'vue-lang-code-flags'

export default {
    name: 'ShowCard',
    components: {
        LangFlag
    },
    props: ['show'],
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
                ],
                unaviablePoster: 'background-image: url(../assets/images/netflix.jpg)'
        }
    },
    computed: {
        rating() {
            return Math.ceil(this.show.vote_average / 2);
        }
    },
    methods: {
        replacePath() {
            if (this.show.poster_path == null) {
                return `background-image: url(${require('../assets/images/netflix.jpg')})`;
            } else {
                return `background-image: url(https://image.tmdb.org/t/p/original${this.show.poster_path})`;
            }
        }
    }
}
</script>

<style scoped lang="scss">
@import '../assets/style/variables.scss';

.card {
    display: inline-block;
    width: 18.75rem;
    height: 28.125rem;
    background-size: cover;
    background-position: center;
    .details {
        opacity: 0;
        padding: 2.5rem .625rem .625rem;
        background-color: rgba(0, 0, 0, 0.8);
        box-shadow: 0 0 0 2px rgba(0,0,0,0.8);
        .fw-bold {
            color: $secondaryText;
            font-size: 1.125rem;
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