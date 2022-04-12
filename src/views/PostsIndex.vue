<template>
  <div class="posts">
    <!-- <h1 v-bind:class="className">{{ message }} Post Count: {{ posts.length }}</h1> -->
    <div v-for="post in posts" v-bind:key="post.id">
      <h3>{{ post.title }}</h3>
      <router-link v-bind:to="`/posts/${post.id}`">
        <img v-bind:src="post.image" v-bind:alt="post.title" style="max-width: 250px" />
      </router-link>
      <div>
        <p>{{ post.body }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Posts",
      posts: [],
    };
  },
  created: function () {
    this.indexPosts();
  },
  methods: {
    indexPosts() {
      axios.get("/posts").then((response) => {
        console.log(response.data);
        this.posts = response.data;
      });
    },
  },
};
</script>
