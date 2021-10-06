<template>
    <header>
        <form>
            <input type="text" v-model="searchTitle">
            <button type="submit" @click.prevent="$emit('search', searchTitle)">Search</button>
        </form>
        
    </header>
</template>

<script>

export default {
    name: 'Header',
    data() {
        return {
            searchTitle: ''
        }
    }
}
</script>

<style scoped lang="scss">

</style>