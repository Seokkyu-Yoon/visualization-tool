<template>
  <b-button-group size="sm">
    <b-button @click="changeMap(0)"> 일반 </b-button>
    <!-- <b-button @click="changeMap(1)"> 그레이</b-button> -->
    <b-button @click="changeMap(2)"> 야간</b-button>
    <b-button @click="changeMap(3)"> 위성 </b-button>
  </b-button-group>
</template>

<script>
import * as maptalks from 'maptalks';
const urlTemplates = [
  'http://xdworld.vworld.kr:8080/2d/Base/201411/{z}/{x}/{y}.png',
  'http://xdworld.vworld.kr:8080/2d/gray/201411/{z}/{x}/{y}.png',
  'http://xdworld.vworld.kr:8080/2d/midnight/201411/{z}/{x}/{y}.png',
  'http://xdworld.vworld.kr:8080/2d/Satellite/service/{z}/{x}/{y}.jpeg',
]
export default {
  name: 'uniq-map-changer',
  props: {
    map: Object
  },
  methods: {
    changeMap(type = 0) {
      this.map.setBaseLayer(
        new maptalks.TileLayer('base', {
          urlTemplate: urlTemplates[type],
        }))
    }
  }
}
</script>
