<template>
  <div id="show-blogs">
    <h1>All Blog Article</h1>
    <div v-for="blog in blogs" class="single-blog">
      <h2>{{ blog.title }}</h2>
      <article>{{ blog.body }}</article>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      blogs: []
    };
  },
  methods: {},
  created() {
    this.$http
      .get("https://jsonplaceholder.typicode.com/posts")
      .then(function(data) {
        //console.log(data); slice it means only return 10 elements of the array(100) body is returned in the response.
        this.blogs = data.body.slice(0, 10);
      });
  }
};
</script>

<style>
#show-blogs {
  /* these CSS rules will centralize on the page */
  max-width: 800px;
  margin: 0 auto;
}
.single-blog {
  padding: 20px;
  margin: 20px 0;
  box-sizing: border-box;
  background: #eee; /*very light gray */
}
</style>
