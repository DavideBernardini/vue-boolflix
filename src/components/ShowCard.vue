<template>
    <ul>
        <li>
            Title: {{show.name}}
        </li>
        <li v-if="show.name.toLowerCase() != show.original_name.toLowerCase()">
            Original name: {{show.original_name}}
        </li>
        <li>
            <span>Lang:  </span>  
            <lang-flag :iso="`${show.original_language}`" :class="{unaviable_flag : aviableFlags.includes(this.show.original_language) == false}"/>
        </li>
        <li>
            Vote: {{show.vote_average}}
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
                ]
        }
    }
}
</script>

<style scoped lang="scss">
ul {
    display: inline-block;
    span {
        vertical-align: middle;
    }
    .unaviable_flag {
        background-image: url(https://upload.wikimedia.org/wikipedia/commons/3/35/Orange_question_mark.svg) !important;
}
}

</style>