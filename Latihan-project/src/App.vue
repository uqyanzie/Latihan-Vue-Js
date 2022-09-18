<script>
export default {
  name: 'app',
  data() {
    return {
      count: 0,
      topic: '',
      api_key: '498a36f1e7a74d49b9941c150df29bd8',
      url_base: `https://newsapi.org/v2/`,
      newsList: []
    }
  },
  methods: {
    fetchNews(e) {
      if (e.key == "Enter") {
        fetch(`${this.url_base}everything?q=${this.topic}&apiKey=${this.api_key}`)
          .then(res => {
            return res.json()

          }).then(this.setResults)
      }
    },
    setResults(results) {
      this.newsList = results.articles
    },
    toArticle(article) {
      let index = this.newsList.indexOf(article)
      window.location.href = this.newsList[index].url
    }
  }
}
</script>

<template>
  <div id="app">
    <main>
      <div class="search-box">
        <label for="topic">Type any topic!</label>
        <input id="topic" type="text" v-model="topic" class="search-bar" placeholder="Search News..."
          @keypress="fetchNews" />
      </div>

      <ul>
        <li v-for="article in newsList" v-on:click="toArticle(article)">
          <img :src="article.urlToImage">
          <h3>{{article.title}}</h3>
          <p>{{article.description}}</p>
        </li>
      </ul>

    </main>
  </div>

</template>

<style>
body {
  font-family: 'montserrat', sans-serif;
}

.title {
  text-align: center;
}

.search-box {
  display: flex;
  flex-direction: column;
  width: 90vw;
  margin: 20px auto;
  justify-content: center;
}

label {
  font-size: 30px;
  margin: 15px 0 20px 20px;
}

.search-bar {
  width: 85vw;
  font-size: 20px;
  margin: 8px 0;
  padding: 15px 25px;
  border-radius: 8px;
}

ul {
  list-style-type: none;
  margin-left: 50px;
  margin-right: 50px;
}

h3 {
  font: bold 20px/1.5 Helvetica, Verdana, sans-serif;
}

li img {
  float: left;
  display: block;
  margin: 0 15px 0 0;
  max-width: 225px;
}

li p {
  font: 200 12px/1.5 Georgia, Times New Roman, serif;
  font-size: 16px;
}

li {
  padding: 10px;
  overflow: hidden;
}

li:hover {
  background: #eee;
  cursor: pointer;
}
</style>