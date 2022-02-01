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

    <div class="wraps">
      <label>
        <i class="fas fa-search-location"></i> 關鍵字搜尋：
        <input type="text" placeholder="請輸入關鍵字" v-model="keywords">
      </label>
    </div>

    <ul class="store-lists">
      <li class="store-info wraps"
        v-for="store in filteredStores"
        :key="`store_${store.id}`"
        @click="triggerPopup(store.id)"
      >
        <h1 v-html="keywordHighlight(store.name)"></h1>

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

        <button class="btn-store-detail" @click="openInfoBox(store.id)">
          <i class="fas fa-info-circle"></i>
          看詳細資訊
        </button>
      </li>
    </ul>
  </div>
</template>

<script>
import { toRefs, inject, watch, computed } from "vue";

export default {
  name: "asideMenu",
  setup() {
    const mapStore = inject('mapStore');
    const map = inject('map');
    const { triggerPopup } = map;
    const { state, setCurrCity, setCurrDistrict, setKeywords, setShowModal, setInfoBoxStoreId } = mapStore;

    const keywordHighlight = val => {
      return val.replace(new RegExp(state.keywords, 'g'), `<span class="highlight">${state.keywords}</span>`)
    };

    const openInfoBox = storeId => {
      setInfoBoxStoreId(storeId);
      setShowModal(true);
    }

    const currCity = computed({
      get () {
        return state.currCity;
      },
      set (value) {
        // 更換行政區回到第一頁
        setCurrCity(value);
      }
    });

    const currDistrict = computed({
      get () {
        return state.currDistrict;
      },
      set (value) {
        // 更換行政區回到第一頁
        setCurrDistrict(value);
      }
    });

    const currKeywords = computed({
      get() {
        return state.keywords;
      },
      set(value) {
        setKeywords(value);
      },
    })

    watch(() => (state.districtList), v => {
      const [arr] = v;
      setCurrDistrict(arr.name);
    });

    return {
      ...toRefs(state),
      currCity,
      currDistrict,
      currKeywords,
      triggerPopup,
      openInfoBox,
      keywordHighlight
    };
  },
};
</script>

<style>
.highlight {
  color: #f08d49;
}
</style>
