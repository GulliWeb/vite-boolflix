<script setup>
// Importo i miei componenti
import AppFooter from './components/AppFooter.vue';
import AppHeader from './components/AppHeader.vue';
import AppMain from './components/AppMain.vue';
</script>

<template>
  <AppHeader/>
  <AppMain/>
  <AppFooter/>
</template>

<style lang="scss" scoped>
@use "./styles/general.scss" as *;
@use 'bootstrap'
</style>
