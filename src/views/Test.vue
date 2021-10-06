<template>
  <div class="test">
    <h1>This is my testing page</h1>
    <button v-on:click="homePage">Click here to see this!</button>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
    };
  },
  created: function () {},
  methods: {
    homePage() {
      this.$router.push("/");
    },
  },
};
</script>
