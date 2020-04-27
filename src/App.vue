<template>
  <div id="app">
    <vue-simple-map-selector
      @selected="selected"
      class="map"
    />
    {{ pref }}
  </div>
</template>

<script>
import VueSimpleMapSelector from './components/VueSimpleMapSelector.vue'

export default {
  name: 'App',
  components: {
    VueSimpleMapSelector
  },
  data () {
    return {
      pref: null
    }
  },
  methods: {
    selected (pref) {
      console.log(pref)
      this.pref = pref && pref.name
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  background: silver;
  padding: 8px 0;
}

.map {
  width: 100vw;
  max-width: 960px;
  height: calc(75vw);
  max-height: 720px;
  padding: 0.5vw;
  margin: 16px auto;
  grid-auto-columns: 12%;
  background: white;
}

.map .pref {
  background: silver;
  color: black;
}

.map .pref.hokkaido {
  background: gold;
}

.map .pref[data-region="kanto"] {
  background: green;
}

.map .pref:hover {

}

.map .pref[data-selected] {

}
</style>
