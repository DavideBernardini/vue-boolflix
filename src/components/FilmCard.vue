<template>
    <ul>
        <li>
            Title: {{movie.title}}
        </li>
        <li v-if="movie.title.toLowerCase() != movie.original_title.toLowerCase()">
            Original title: {{movie.original_title}}
        </li>
        <li>
            <span>Lang:  </span>  
            <lang-flag 
            :iso="`${movie.original_language}`" 
            :class="{unaviable_flag : aviableFlags.includes(this.movie.original_language) == false}"/>
        </li>
        <li>
            <i class="fas fa-star" 
            v-for="(n, index) in rating" 
            :key="index"></i>
            <i class="far fa-star" 
            v-for="(n, index) in (5 - rating)" 
            :key="index"></i>
        </li>
    </ul>
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
    }
}
</script>

<style scoped lang="scss">
ul {
    display: inline-block;
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