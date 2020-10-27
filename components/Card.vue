<template>
  <div class="card">
    <img :src="urlCardToImage" class="card-img-top" alt="#" />
    <div class="card-body">
      <h3 class="card-title">
        {{ cardTitle }}
      </h3>
      <p class="card-text-description">
        {{ cardDescription }}
      </p>
      <p class="card-text-author">
        {{ cardAuthor }}
      </p>
      <p class="card-text-publish">
        {{ cardPublishedAt }}
      </p>
      <a :href="cardUrl" class="btn btn-primary" @click="$emit('card-click')">Click For More</a>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    urlCardToImage: "",
    cardTitle: "",
    cardDescription: "",
    cardAuthor: "",
    cardPublishedAt: "",
    cardUrl: "",
  },
};
</script>

<style>
.card {
  width: 0 auto;
  height: 40rem;
  margin: 60px 20px 20px 10px;
  font-family: sans-serif;
  text-align: justify;
}
.card-body {
  width: auto;
}
.card-img-top {
  height: 18rem;
  object-fit: cover;

}
.card-title {
  font-size: 16px;
}
.card-text-description {
  font-size: 13px;
}
.card-text-author {
  font-weight: bold;
}
.card-text-publish {
  font-size: 11px;
}
.card-text-content {
  font-size: 12px;
}
.btn {
  color: white !important;
  font-size: 14px;
}
</style>