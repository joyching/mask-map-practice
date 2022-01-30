<template>
  <div id="app">
    <asideMenu />

    <div class="mask-map" id="mask-map"></div>

    <lightbox />
  </div>
</template>

<script>
import { mapActions } from 'vuex';
import asideMenu from './components/asideMenu.vue';
import lightbox from './components/lightbox.vue';

export default {
  components: {
    asideMenu,
    lightbox
  },
  name: 'App',
  methods: {
    ...mapActions(['fetchLocations', 'fetchPharmacies'])
  },
  mounted() {
    this.fetchLocations();
    this.fetchPharmacies();
  }
}
</script>

<style lang="scss" src="./style.scss"></style>
