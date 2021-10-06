<template>
  <div class="postnew">
    <h1>New Blog Post</h1>
    <form v-on:submit.prevent="createPost()">
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      Title:
      <input type="text" v-model="newPostParams.title" />
      Image Url:
      <input type="text" v-model="newPostParams.image" />
      Body:
      <input type="text" v-model="newPostParams.body" />
      <input type="submit" value="Create" />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      newPostParams: {},
      errors: [],
    };
  },
  created: function () {},
  methods: {
    createPost: function () {
      axios
        .post("/posts", this.newPostParams)
        .then((response) => {
          console.log("posts create", response);
          this.$router.push("/posts");
        })
        .catch((error) => {
          console.log("posts create error", error.response);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
