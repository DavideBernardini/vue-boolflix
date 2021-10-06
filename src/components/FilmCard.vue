<template>
    <ul>
        <li>
            Title: {{movie.title}}
        </li>
        <li v-if="movie.title.toLowerCase() != movie.original_title.toLowerCase()">
            Original title: {{movie.original_title}}
        </li>
        <li>
            <lang-flag :iso="`${movie.original_language}`"/>
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
    props: ['movie']
}
</script>

<style scoped lang="scss">

</style>