<template>
  <div class="home">
    <h1>{{ post.title }}</h1>
    <img v-bind:src="post.image" alt="" />
    <p>{{ post.body }}</p>
    <router-link v-bind:to="`/posts/${post.id}/edit`">Edit Post</router-link>
    |
    <router-link to="/posts">Back to all recipes</router-link>
    |
    <button v-on:click="destroyPost(post)">Delete Post</button>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      post: {},
    };
  },
  created: function () {
    this.showPost();
  },
  methods: {
    showPost: function () {
      axios.get("/posts/" + this.$route.params.id).then((response) => {
        this.post = response.data;
        console.log(this.post);
      });
    },
    destroyPost: function (post) {
      axios.delete("http://localhost:3000/posts/" + post.id).then((response) => {
        console.log("Success", response.data);
        this.$router.push("/posts");
      });
    },
  },
};
</script>
