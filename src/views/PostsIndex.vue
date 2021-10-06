<template>
  <div class="PostsIndex">
    <h1>All Blog Posts</h1>
    <div v-for="post in posts" v-bind:key="post.id">
      <h4>
        {{ post.title }}
      </h4>
    </div>
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
    this.postsIndex();
  },
  methods: {
    postsIndex: function () {
      axios.get("http://localhost:3000/posts").then((response) => {
        console.log(response.data);
        this.posts = response.data;
      });
    },
  },
};
</script>
