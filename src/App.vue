<template>
  <!-- <add-blog></add-blog> -->
  <!-- <show-blogs></show-blogs> -->
  <!-- new routes -->
  <router-view></router-view>
</template>

<script>
import addBlog from "./components/addBlog.vue";
import showBlogs from "./components/showBlogs";

export default {
  components: {
    "add-blog": addBlog,
    "show-blogs": showBlogs
  }
};
</script>

<style>
</style>
