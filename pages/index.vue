]<template>
  <div class="">
    <NavbarTop/>
    <div class="card-columns">
      <div v-for="(item, index) in articles" :key="index">
        <Card
          :cardTitle="item.title"
          :urlCardToImage="item.urlToImage"
          :cardDescription="item.description"
          :cardAuthor="item.author"
          :cardPublishedAt="item.publishedAt"
          @card-click="openNews(item)"
        />
      </div>
    </div>
    <div class="button-load text-center">
      <button class="button btn-primary" @click="loadMore">Load More</button>
    </div>
    <Footer/>
  </div>
</template>

<script>
import Navbar from "~/components/Navbar.vue";
import Card from "~/components/Card.vue";
import Footer from "~/components/Footer.vue";
import axios from "axios";
export default {
  components: {
    NavbarTop: Navbar,
    Card: Card,
    Footer: Footer,
  },
  data() {
    return {
      dataArticles: [],
      articles: [],
      current: 3,
    };
  },
  mounted() {
    this.getDataArticles();
  },
  methods: {
    getDataArticles() {
      axios
        .get(
          'https://beritaku-api.herokuapp.com/articles'
        )
        .then(res => {
          console.log(res);
          this.dataArticles = res.data
          res.data.map((item, key) => {
            if (item.description !== null && this.articles.length < 3) {
              this.articles.push(item)
            }
          });
        })
        .catch((err) => {
          console.log(err);
        });
    },
    loadMore() {
      this.articles = [];
      this.current += 3;
      this.dataArticles.map((item, key) => {
        item.description !== null && this.articles.length < this.current
          ? this.articles.push(item)
          : "";
        this.isOpen == true ? console.log("Hello Bray!") : "";
      });
    },
    openNews(item) {
      this.$router.push(`/detail?id=${item.id}`)
    }
  },
};
</script>

<style>
.navbar {
  width: 100%;
}
.content {
  width: 100%;
  height: auto;
}
@media (min-width: 768px) {
  .card-columns {
    width: auto;
    column-count: 3;
  }
}
/* Large devices (desktops, 992px and up) */
@media (min-width: 992px) {
  .card-columns {
    column-count: 3;
  }
}

/* Extra large devices (large desktops, 1200px and up) */
@media (min-width: 1200px) {
  .card-columns {
    column-count: 3;
  }
}
@media (max-width: 768px) {
  .card {
    padding-top: 50px;
    margin: 0 auto!important;
  }
}
@media (max-width: 768px) {
  .img-top {
    margin: 0 auto!important;
  }
}
.button-load {
  margin-top: 40px;
}
.button:hover {
  color: lightgrey;
  border-color: white !important;
}
</style>
