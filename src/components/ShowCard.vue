<template>
    <div class="card" :style="replacePath()">
        <h2>
            Title: {{show.name}}
        </h2>
        <h3 v-if="show.name.toLowerCase() != show.original_name.toLowerCase()">
            Original name: {{show.original_name}}
        </h3>
        <div>
            <span>Lang:  </span>  
            <lang-flag 
            :iso="`${show.original_language}`" 
            :class="{unaviable_flag : aviableFlags.includes(this.show.original_language) == false}"/>
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
    },
    methods: {
        replacePath() {
            if (this.show.poster_path == null) {
                return 'background-image: url(https://i.pinimg.com/originals/eb/aa/44/ebaa441df578a3e48e26ef1a15a04e3c.jpg)'
            } else {
                return `background-image: url(https://image.tmdb.org/t/p/original${this.show.poster_path})`;
            }
        }
    }
}
</script>

<style scoped lang="scss">

.card {
    display: inline-block;
    width: 18.75rem;
    height: 28.125rem;
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