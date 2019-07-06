<template>
<div class="col-md-7 news-section">
    <h1 class="display-4" v-if="source">
        LATEST <span>NEWS</span>
    </h1>
    <div class="loading" v-if="loading">
        Loading...
    </div>
    <div v-if="!loading">
        <a v-bind:href="article.url" v-for="article in articles" target="_blank">
            <div class="grid-item">
            <p class="badge badge-light">{{article.author}}</p>
            <img v-bind:src="article.urlToImage" alt="">
            <p class="title"> {{article.title}} </p>
            <p class="desc"> {{article.description}} </p>
            <hr>
        </div>
        </a>
    </div>
</div>
</template>

<script>
export default {
  name: "NewsList",
  props: ["source"],
  methods: {
    updateNews: function(source) {
      this.loading = true;
      this.$http
        .get(
          "https://newsapi.org/v1/articles?source=" +
            source +
            "&apiKey=d4850e40dbe941518185860fd3a35655"
        )
        .then(response => {
          this.loading = false;
          this.articles = response.data.articles;
        });
    }
  },
  data() {
    return {
      articles: [],
      loading: false
    };
  },
  watch: {
    source: function(val) {
      this.updateNews(val);
    }
  }
};
</script>

<style scoped>
.news-section {
  overflow-y: scroll;
  padding: 3em 2em;
}

span {
  font-weight: 800;
}
h1 {
  text-align: center;
}

.grid-item {
  padding: 1.5em 1em;
}

.grid-item .title {
  margin-top: 1em;
  color: #000;
  font-weight: 700;
  text-transform: uppercase;
}

.grid-item .desc {
  color: #333;
  font-size: 14px;
  margin-top: 1.5em;
  padding: 0 0 0 1em;
}

.grid-item img {
  display: block;
  width: 70%;
  height: auto;
}

@media screen and (max-width: 1000px) {
  .grid-item img {
    width: 80%;
  }
}

@media screen and (max-width: 768px) {
  .news-section {
    overflow-y: auto;
    padding: 3em 2em;
  }
}

@media screen and (max-width: 500px) {
  .grid-item img {
    width: 90%;
    margin: 0 auto;
  }

  .news-section {
    padding: 3em 1em;
  }
}
</style>
