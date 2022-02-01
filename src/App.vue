<template>
  <div id="app">
    <asideMenu />

    <maskMap />

    <lightbox />
  </div>
</template>

<script>
import { provide } from 'vue';
import map from '@/composition/map';
import mapStore from '@/composition/store';

import asideMenu from './components/asideMenu.vue';
import lightbox from './components/lightbox.vue';
import maskMap from './components/maskMap.vue';

export default {
  name: 'App',
  components: {
    asideMenu,
    lightbox,
    maskMap
  },
  setup () {
    provide('mapStore', mapStore);
    provide('map', map);

    mapStore.fetchLocations();
    mapStore.fetchPharmacies();
  }
}
</script>

<style lang="scss" src="./style.scss"></style>
