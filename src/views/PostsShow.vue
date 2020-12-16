<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h1>{{ post.title }}</h1>
    <h4>{{ post.body }}</h4>
    <img v-bind:src="post.image">
    
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      post: [],
    };
  },
  created: function () {
    this.postsShow();
  },
  methods: {
    postsShow: function () {
      console.log("in posts show");
      axios.get("/api/posts/4").then((response) => {
        console.log(response.data);
        this.post = response.data;
      });
    },
  },
};
</script>