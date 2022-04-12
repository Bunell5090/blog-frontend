<template>
  <div class="home">
    <h1>Post Info</h1>
    <p>Title: {{ posts.title }}</p>
    <p>Body: {{ posts.body }}</p>
    <p>Image: {{ posts.image }}</p>
    <router-link v-bind:to="`/posts/${posts.id}/edit`" style="margin-right: 10px">Edit Post</router-link>
    <button v-on:click="destroyPost()" style="margin-right: 10px">Delete</button>
    <router-link to="/posts">Back to all posts</router-link>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      posts: {},
    };
  },
  created: function () {
    axios.get(`/posts/${this.$route.params.id}`).then((response) => {
      this.posts = response.data;
    });
  },
  methods: {
    destroyPost() {
      axios.delete(`/posts/${this.posts.id}`).then((response) => {
        console.log(response);
        this.$router.push("/posts");
      });
    },
  },
};
</script>
