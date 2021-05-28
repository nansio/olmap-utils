<template>
  <div class="dashboard-container">
    <div class="content-wrapper">
      <div id="mapId" />
      <div class="ops">
        <el-button type="primary" size="small" @click="adjustZoom">谷歌地图</el-button>
        <el-button type="primary" size="small" @click="adjustZoom">百度地图</el-button>
        <el-button type="primary" size="small" @click="adjustZoom">高德地图</el-button>
        <el-button type="primary" size="small" @click="adjustZoom">天地图</el-button>
      </div>
    </div>
  </div>
</template>

<script>

// import { mapGetters } from 'vuex'

import 'ol/ol.css'
import { Map, View } from 'ol'
import TileLayer from 'ol/layer/Tile'
import XYZ from 'ol/source/XYZ'
// import OSM from 'ol/source/OSM'

export default {
  name: 'Dashboard',
  // computed: {
  //   ...mapGetters([
  //     'name'
  //   ])
  // }
  data() {
    return {
      map: null
    }
  },
  mounted() {
    this.initMap()
  },
  methods: {
    initMap() {
      const gaodeLayer = new TileLayer({
        source: new XYZ({
          url: 'http://webst0{1-4}.is.autonavi.com/appmaptile?lang=zh_cn&size=1&scale=1&style=7&x={x}&y={y}&z={z}'
        })
      })
      this.map = new Map({
        target: 'mapId',
        layers: [
          gaodeLayer
          // new TileLayer({
          //   source: new OSM()
          // })
        ],
        view: new View({
          center: [116.420774, 39.481276],
          zoom: 3,
          multiWorld: false
        })
      })
    },
    adjustZoom() {
      this.map.getView().adjustZoom(2)
    },
    switch2Gaode() {
      // const gaodeLayer = new TileLayer({
      //   source: new XYZ({
      //     url: 'http://webst0{1-4}.is.autonavi.com/appmaptile?lang=zh_cn&size=1&scale=1&style=7&x={x}&y={y}&z={z}'
      //   })
      // })
    }
  }
}
</script>

<style lang="scss" scoped>
.dashboard-container {
  max-height: calc(100vh - 50px);
  width: 100%;
  .content-wrapper{
    // display: flex; flex-flow: row nowrap;
    // justify-content: space-between;
    // align-items: flex-start;
    #mapId{
      border: 5px dashed darkorange;
      box-sizing: border-box;
      height: calc(100vh - 360px);
      width: 100%;
    }
    .ops{
      background-color: rgba($color: #808080, $alpha: 0.3);
      height: 310px; width: 100%;
      text-align: center; line-height: 300px;
    }
  }
}
</style>
