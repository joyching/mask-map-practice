<template>
  <div id="app">
    <asideMenu @triggerMarkerPopup="openPopup" ref="menu" />

    <maskMap ref="map" />

    <lightbox />
  </div>
</template>

<script>
import { mapActions } from 'vuex';
import asideMenu from './components/asideMenu.vue';
import lightbox from './components/lightbox.vue';
import maskMap from './components/maskMap.vue';

export default {
  components: {
    asideMenu,
    lightbox,
    maskMap
  },
  name: 'App',
  methods: {
    ...mapActions(['fetchLocations', 'fetchPharmacies']),
    openPopup(id) {
      this.$refs.map.triggerPopup(id);
    }
  },
  mounted() {
    this.fetchLocations();
    this.fetchPharmacies();
  }
}
</script>

<style lang="scss" src="./style.scss"></style>
