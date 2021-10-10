<template>
    <header class="px-4 d-flex align-items-center justify-content-between">
            <img src="../assets/images/netflix-logo.png" alt="" class="logo">
            <div class="search d-flex">
                <transition name="fade">
                    <input type="text" class="form-control" placeholder="Cerca film o serie tv"
                    v-if="show"
                    v-model="searchTitle" @keyup="$emit('search', searchTitle)">
                </transition>
                <button @click="show = !show">
                    <i class="fas fa-search ms-2"></i>
                </button>
            </div>
    </header>
</template>

<script>

export default {
    name: 'Header',
    data() {
        return {
            searchTitle: '',
            show: true
        }
    }
}
</script>

<style scoped lang="scss">
@import '../assets/style/variables.scss';

header {
    height: 70px;
    .logo {
        height: 60%;
    }
    .form-control:focus {
        box-shadow: unset;
    }
    button {
        background-color: unset;
        color: $secondaryText;
        border: none;
        font-size: 25px;
    }
    .fade-enter-active, .fade-leave-active {
        transition: opacity .2s;
    }
    .fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
        opacity: 0;
    }
}
</style>