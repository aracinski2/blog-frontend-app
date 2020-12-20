<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h1>{{ post.title }}</h1>
    <h4>{{ post.body }}</h4>
    <img v-bind:src="post.image">
    <h1>User id? {{ $parent.getUserId() }}</h1>
    <h1>User id of post? {{ post.user_id }}</h1>
    <!-- <p><button v-on:click="postsDestroy()">Delete</button></p> -->
    <router-link v-if="$parent.getUserId() == post.user_id" v-bind:to="`/posts/${post.id}/edit`">Edit</router-link>

    <button v-if="$parent.getUserId() == post.user_id" v-on:click="postsDestroy()">Delete</button>

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
      axios.get("/api/posts/" + this.$route.params.id).then((response) => {
        console.log(response.data);
        this.post = response.data;
      });
    },
    postsDestroy: function () {
      console.log("destroying a post");
      axios.delete(`/api/posts/${this.post.id}`).then((response) => {
        console.log(response.data);
        this.$router.push("/posts");
      });
    },
  },
};
</script>