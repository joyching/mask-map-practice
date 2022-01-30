<template>
  <div class="aside-menu">
    <div class="wraps">
      <label>
        縣市：<select v-model="currCity">
          <option v-for="city in cityList" :key="`city_${city}`">{{ city }}</option>
        </select>
      </label>

      <label>
        行政區：<select v-model="currDistrict">
          <option v-for="district in districtList" :key="`district_${district.id}`">{{ district.name }}</option>
        </select>
      </label>
    </div>

    <ul class="store-lists">
      <li class="store-info wraps"
        v-for="store in filteredStores"
        :key="`store_${store.id}`"
      >
        <h1>{{ store.name }}</h1>

        <div class="mask-info">
          <i class="fas fa-head-side-mask"></i>
          <span>大人口罩: {{ store.mask_adult }} 個</span>
        </div>

        <div class="mask-info">
          <i class="fas fa-baby"></i>
          <span>兒童口罩: {{ store.mask_child }} 個</span>
        </div>

        <div class="mask-info">
          最後更新時間: {{ store.updated }}
        </div>

        <button class="btn-store-detail">
          <i class="fas fa-info-circle"></i>
          看詳細資訊
        </button>
      </li>
    </ul>
  </div>
</template>

<script>
import { mapGetters, mapState } from 'vuex';

export default {
  name: 'asideMenu',
  computed: {
    currCity: {
      get() {
        return this.$store.state.currCity;
      },
      set(value) {
        this.$store.commit('setcurrCity', value);
      },
    },
    currDistrict: {
      get() {
        return this.$store.state.currDistrict;
      },
      set(value) {
        this.$store.commit('setcurrDistrict', value);
      },
    },
    ...mapGetters(['cityList', 'districtList', 'filteredStores'])
  },
  watch: {
    districtList(v) {
      const [arr] = v;
      this.currDistrict = arr.name;
    },
  },
}
</script>
