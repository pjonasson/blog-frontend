<template>
  <div class="postnew">
    <h1>Edit Blog Post</h1>
    <form v-on:submit.prevent="updatePost()">
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      Title:
      <input type="text" v-model="editPostParams.title" />
      Image Url:
      <input type="text" v-model="editPostParams.image" />
      Body:
      <input type="text" v-model="editPostParams.body" />
      <input type="submit" value="Update" />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      editPostParams: {},
      errors: [],
    };
  },
  created: function () {
    this.showPost();
  },
  methods: {
    showPost: function () {
      axios.get("/posts/" + this.$route.params.id).then((response) => {
        this.editPostParams = response.data;
        console.log(this.editPostParams);
      });
    },
    updatePost: function () {
      axios
        .patch("/posts/" + this.$route.params.id, this.editPostParams)
        .then((response) => {
          console.log("posts updated", response.data);
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
