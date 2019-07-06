<template>
<div class="col-md-7 news-section">
    welcome to contact page
</div>
</template>

<script>
export default {
  name: "ContactUs",
  props: ["source"],
};
</script>

<style scoped>
.news-section {
  overflow-y: scroll;
  padding: 3em 2em;
}

.loading {
  width: 20px;
  height: 20px;
  border-radius: 50%;
  border-top-color: blue;
  animation: rotateBox 0.5s forwards infinite;
}

@keyframes rotateBox {
  to {
    transform: rotate(360deg);
  }
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
