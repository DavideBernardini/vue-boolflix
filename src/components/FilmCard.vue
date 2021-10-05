<template>
    <ul>
        <li>movie.title</li>
        <li>movie.original_title</li>
        <li>movie.original_language</li>
        <li>movie.vote_average</li>
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