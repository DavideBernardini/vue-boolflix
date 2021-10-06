<template>
    <ul>
        <li>
            Title: {{movie.title}}
        </li>
        <li v-if="movie.title.toLowerCase() != movie.original_title.toLowerCase()">
            Original title: {{movie.original_title}}
        </li>
        <li>
            <span>Lang:</span>  <lang-flag :iso="`${movie.original_language}`" :class="{unaviable_flag : aviableFlags.includes(this.movie.original_language) == false}"/>
        </li>
        <li>
            Vote: {{movie.vote_average}}
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
    }
}
</script>

<style scoped lang="scss">
span {
    vertical-align: middle;
}
.unaviable_flag {
    background-image: url(https://upload.wikimedia.org/wikipedia/commons/3/35/Orange_question_mark.svg) !important;
}
</style>