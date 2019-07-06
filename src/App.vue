<template>
  <div id="app" class="row">
    <SourceSelection v-on:SourceChanged="SourceChanged"></SourceSelection>
    <router-view v-bind:source="source"></router-view>
    <!-- <NewsList v-bind:source="source"></NewsList> -->
  </div>
</template>

<script>
import SourceSelection from "./components/SourceSelection";

import NewsList from "./components/NewsList";

export default {
  name: "App",
  components: {
    SourceSelection,
    NewsList
  },
  data() {
    return {
      source: ""
    };
  },
  methods: {
    SourceChanged: function(source) {
      this.source = source;
    }
  }
};
</script>

<style>
#app {
  background: #f1f2f3;
  width: 100%;
  max-height: calc(100vh - 90px);
}

.row {
  margin-right: 0;
  margin-left: 0;
}

@media screen and (max-width: 768px) {
  #app {
  max-height: none;
}
}

@media screen and (max-width: 500px) {
  #app {
  text-align: center;
}
}
</style>
