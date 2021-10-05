<template>
    <ul>
        <li v-if="movie.title.toLowerCase() != movie.original_title.toLowerCase()">
            Title: {{movie.title}}
        </li>
        <li>
            Original title{{movie.original_title}}
        </li>
        <li>
            Lang: {{movie.original_language}}
        </li>
        <li>
            Vote: {{movie.vote_average}}
        </li>
    </ul>
</template>

<script>

export default {
    name: 'FilmCard',
    props: ['movie']
}
</script>

<style scoped lang="scss">

</style>