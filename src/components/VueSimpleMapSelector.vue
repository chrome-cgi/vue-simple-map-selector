<template>
  <div class="vue-simple-map-selector" :style="mapStyle()" @click="clicked(null)">
    <div
      v-for="(pref, i) in prefs"
      :key="i"
      :style="style(pref)"
      class="pref"
      :class="pref.key"
      :data-pref="pref.key"
      :data-region="pref.regionKey"
      :data-isocode="pref.isoCode"
      :data-selected="pref.key === selectedPref"
      @click.stop="clicked(pref)"
    >
      {{ pref.displayName }}
    </div>
  </div>
</template>

<script>
import JapanPrefectures from '../assets/japan-prefectures.json'

export { JapanPrefectures }

export default {
  name: 'vue-simple-map-selector',
  props: {
    prefs: {
      type: Array,
      default () {
        return JapanPrefectures
      }
    }
  },
  data () {
    return {
      selectedPref: null
    }
  },
  computed: {
    mapGridW () {
      return this.prefs.map(pr => pr.pos.x + pr.pos.w).reduce((a, b) => Math.max(a, b))
    },
    mapGridH () {
      return this.prefs.map(pr => pr.pos.y + pr.pos.h).reduce((a, b) => Math.max(a, b))
    }
  },
  methods: {
    style (pref) {
      return {
        gridColumn: `${pref.pos.x + 1} / span ${pref.pos.w}`,
        gridRow: `${pref.pos.y + 1} / span ${pref.pos.h}`
      }
    },
    mapStyle () {
      return {
        gridAutoColumns: `${100 / this.mapGridW + '%'}`,
        gridAutoRows: `${100 / this.mapGridH + '%'}`
      }
    },
    clicked (pref) {
      this.selectedPref = pref && pref.key
      this.$emit('selected', pref)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.vue-simple-map-selector {
  display: grid;
  box-sizing: border-box;
}

.pref {
  border-style: none solid solid none;
  border-color: white;
  border-width: 1px;
  display: flex;
  justify-content: center;
  align-items: center;
  background: #888;
  font-size: clamp(8px, 1.5vw, 18px);
  color: white;
  line-height: 1.2;
  user-select: none;
}

.pref:hover {
  opacity: 0.5;
  cursor: pointer;
}

[data-region="hokkaido"] { background: #4040BF; }
[data-region="tohoku"]   { background: #4088BF; }
[data-region="kanto"]    { background: #40BFAE; }
[data-region="chubu"]    { background: #40BF66; }
[data-region="kansai"]   { background: #62BF40; }
[data-region="chugoku"]  { background: #AABF40; }
[data-region="shikoku"]  { background: #BF8C40; }
[data-region="kyushu"]   { background: #BF4440; }

[data-selected] {
  background: #f33;
  font-weight: bold;
}
</style>
