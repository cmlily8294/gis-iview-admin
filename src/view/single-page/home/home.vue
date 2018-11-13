<template>
  <div id="ol-map">

  </div>
</template>

<script>
import Map from 'ol/Map'
import View from 'ol/View'
import TileLayer from 'ol/layer/Tile'
import {OSM, TileArcGISRest} from 'ol/source'
import ZoomSlider from 'ol/control/ZoomSlider'
import './home.module.less'
import 'ol/ol.css'
export default {
  name: 'home',
  components: {
  },
  data () {
    return {
    }
  },
  mounted () {
    this.$nextTick(() => {
      this.initMap()
    })
  },
  methods: {
    initMap () {
      const url = 'https://sampleserver1.arcgisonline.com/ArcGIS/rest/services/' +
          'Specialty/ESRI_StateCityHighway_USA/MapServer'

      const layers = [
        new TileLayer({
          source: new OSM()
        }),
        new TileLayer({
          extent: [-13884991, 2870341, -7455066, 6338219],
          source: new TileArcGISRest({
            url: url
          })
        })
      ]
      const map = new Map({
        layers: layers,
        target: 'ol-map',
        view: new View({
          center: [-10997148, 4569099],
          zoom: 4
        })
      })
      map.addControl(new ZoomSlider())
    }
  }
}
</script>
