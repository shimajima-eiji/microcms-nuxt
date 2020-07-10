<template>
  <section>
    <div class="news">
      <ul>
        <li class="news__article" v-for="article in articles" :key="article.id">
          <p>{{ modifyDatetime(article.createdAt) }}</p>
          <h2 class="news__articleTitle">{{ article.title }}</h2>
          <div class="news__articleBody" v-html="article.body"></div>
        </li>
      </ul>
    </div>
  </section>
</template>

<script>
import axios from "axios";
import marked from "marked";

export default {
  components: {},
  data() {
    return {
      articles: []
    };
  },
  methods: {
    fetchArticles() {
      axios
        .get(process.env.ENDPOINT,  {
          headers: { "X-API-KEY": process.env.API_KEY }
        })
        .then(res => {
          console.log(res.data);
          this.articles = res.data.contents;
          this.articles.map((article) => article.body = marked(article.body));
        })
        .catch(err => {
          console.log(err);
        });
    },
    modifyDatetime(date) {
      const Ymd = date.split("T")[0];
      const His = date.split("T")[1].split(".")[0];

      return Ymd + " " + His;
    }
  },
  mounted() {
    this.fetchArticles();
  }
};
</script>

<style scoped>
.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 400;
  font-size: 100px;
  color: #2E495E;
  letter-spacing: 1px;
  font-size: 6em;
}

li {
  list-style-type: none;
}

.news__articleBody {
  background: #efefef;
  padding: 20px;
  text-align: left;
}
</style>

