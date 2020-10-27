<template>
  <div class="container">
    <NavbarTop/>
    <div class="card" style="padding-top: 100px; width: 100%">
      <h3 style="padding: 16px; text-align: center;">{{ currentArticles.title }}</h3>
      <img :src="currentArticles.urlToImage" class="img-top" alt="" style="width: 100%" />
      <br />
      <br />
      <p style="padding: 16px; text-align: justify;">
        {{ currentArticles.description }}
      </p>
      <h5 style="padding: 16px; text-align: justify;">{{ currentArticles.author }}</h5>
      <br>
      <p style="padding: 16px; text-align: justify;"> {{ currentArticles.content }}</p>
    </div>
  </div>
</template>

<script>
import Navbar from "~/components/Navbar.vue"
import axios from 'axios'
export default {
  components: {
    NavbarTop: Navbar,
  },
  data() {
    return {
      currentArticles: {},
      idArticles: 0
    }
  },
  mounted() {
    this.idArticles = this.$route.query.id
    this.getCurrentArticles()
  },
  methods: {
    getCurrentArticles() {
      axios.get(`https://beritaku-api.herokuapp.com/articles/${this.idArticles}`)
      .then(res => {
        this.currentArticles = res.data
      })
      .catch(err => {
        console.log(err);
      })
    }
  }
}
</script>

<style>
.card {
    height: auto;
}
.img-top {
  object-fit: cover!important;
  padding-bottom: 1rem;
}
</style>