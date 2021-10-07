<template>
    <ul>
        <img :src="`https://image.tmdb.org/t/p/w300${show.poster_path}`" :alt="`${show.title} poster`">
        <li>
            Title: {{show.name}}
        </li>
        <li v-if="show.name.toLowerCase() != show.original_name.toLowerCase()">
            Original name: {{show.original_name}}
        </li>
        <li>
            <span>Lang:  </span>  
            <lang-flag 
            :iso="`${show.original_language}`" 
            :class="{unaviable_flag : aviableFlags.includes(this.show.original_language) == false}"/>
        </li>
        <li>
            <i class="fas fa-star" 
            v-for="(n, index) in rating" 
            :key="index"></i>
            <i class="far fa-star" 
            v-for="(n, index) in (5 - rating)" 
            :key="index + 'empty'"></i>
        </li>
    </ul>
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
                ]
        }
    },
    computed: {
        rating() {
            return Math.ceil(this.show.vote_average / 2);
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