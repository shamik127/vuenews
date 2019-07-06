<template>
<div class="col-md-5 list-select">
<p class="source-select-text">SELECT A SOURCE</p>
<select class="custom-select" v-on:change="sourceChanged">
  <option v-bind:value="source.id" v-for="source in sources"> {{source.name}} </option>
</select>
<div class="description" v-if="source">
    <p class="info"> {{source.description}} </p>
    <a class="btn-custom" v-bind:href="source.url" target="_blank">Go to {{source.name}}</a>
</div>
</div>
</template>

<script>
export default {
  name: "SourceSelection",
  data() {
    return {
      sources: [],
      source: ""
    };
  },
  methods: {
    sourceChanged: function(e) {
      for (var i = 0; i < this.sources.length; i++) {
        if (this.sources[i].id === e.target.value) {
          this.source = this.sources[i];
        }
      }
      this.$emit("SourceChanged", e.target.value);
    }
  },
  created: function() {
    this.$http
      .get("https://newsapi.org/v1/sources?language=en")
      .then(response => {
        //this.sources = response.articles.source;
        this.sources = response.data.sources;
        this.source = this.sources[0];
        this.$emit("SourceChanged", this.source.id);
      })
      .catch(err => {
        console.log(err);
      });
  }
};
</script>

<style scoped>
.description {
  margin-top: 3em;
  font-weight: 800;
  font-size: 14px;
}

p.info {
  margin-bottom: 3em;
  text-decoration: underline;
}

.custom-select {
  margin-top: 3em;
}

.list-select {
  padding: 1em 2em;
  height: calc(100vh - 96px);
}

.btn-custom {
  background: #333;
  padding: 1em 2em;
  color: #ffffff;
}

@media screen and (max-width: 768px) {
  .list-select {
    padding: 1em 2em;
    height: auto;
    min-height: 300px;
  }
}
</style>
