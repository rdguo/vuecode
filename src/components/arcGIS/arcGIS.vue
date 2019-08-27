<template>
  <div id="chartMap" ref="chartMap" style="width: 100%;height: 100vh;"></div>
</template>

<script>
import * as esriLoader from 'esri-loader'
export default {
  components: {
  },
  data: () => ({
  }),
  created () {
    this.createMap()
  },
  methods: {
    createMap () {
      this.loading = false
      esriLoader.loadModules([
        'esri/Map',
        'esri/views/SceneView'
      ]).then(([Map, SceneView]) => {
        this.loading = true
        let map = new Map({
          basemap: 'hybrid',
          ground: 'world-elevation'
        })
        new SceneView({
          map: map,
          container: 'chartMap', // reference to dom node that will contain the view
          scale: 50000000, // Sets the initial scale to 1:50,000,000
          center: [-101.17, 21.78], // Sets the center point of view with lon/lat
          camera: {
            position: [7.654, 45.919, 9184],
            tilt: 80
          }
        })
      }).catch(err => {
        alert('err', err)
      })
    }
  }
}
</script>

<style lang="scss" scoped>
@import url('https://js.arcgis.com/4.6/esri/css/main.css');
</style>
