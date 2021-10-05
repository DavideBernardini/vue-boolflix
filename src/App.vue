<template>
  <div id="app">
    <Header @search="searchTitle"/>
    <Films :srcTitle="titleSearch"/>
  </div>
</template>

<script>
import Header from './components/Header';
import Films from './components/Films';

export default {
  name: 'App',
  components: {
    Header,
    Films
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


</style>
