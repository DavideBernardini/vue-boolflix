<template>
  <div id="app">
    <Header @search="searchTitle"/>
    <Films :srcTitle="titleSearch"/>
    <Shows :srcTitle="titleSearch"/>
  </div>
</template>

<script>
import Header from './components/Header';
import Films from './components/Films';
import Shows from './components/Shows';

export default {
  name: 'App',
  components: {
    Header,
    Films,
    Shows
  },
  data() {
    return {
      titleSearch: ''
    }
    },
    methods: {
      searchTitle(text) {
        this.titleSearch = text;
      }
  }
}
</script>

<style lang="scss">
@import '~@fortawesome/fontawesome-free/css/all.css';
@import './assets/style/common.scss';
</style>
