<template>
  <div v-theme:column="'wide'" id="show-blogs">
    <h1>All Blog Article</h1>
    <input type="text" v-model="search" placeholder="search blogs" />
    <!-- <div v-for="blog in blogs" class="single-blog"> -->
    <div v-for="blog in filteredBlogs" class="single-blog">
      <h2 v-rainbow2>{{ blog.title | toLocaluppercase }}</h2>
      <article>{{ blog.body | snippet }}</article>
    </div>
  </div>
</template>

<script>
// dotdot go up level to go above component folder. we don't need the .js it knows it is a JavaScript file.
import searchMixin from "../mixins/searchMixin";

export default {
  data() {
    return {
      blogs: [],
      search: ""
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
  }, //custom search using computed property instead of filters.
  computed: {
    // mixins replace this.
    // filteredBlogs: function() {
    //   return this.blogs.filter(blog => {
    //     return blog.title.match(this.search);
    //   });
    // }
  },
  //To register filters locally instead of Global filters
  filters: {
    "to-local-uppercase": function(value) {
      return value.toUpperCase();
    },
    // Most developers code it like this insteaf of the one above. to-localbla bla but you need to capitalize the next letter and without the hyphens.
    toLocaluppercase(value) {
      return value.toUpperCase();
    }
  },
  //To register directive locally
  directives: {
    rainbow2: {
      bind(el, binding, vnode) {
        el.style.color =
          "#" +
          Math.random()
            .toString()
            .slice(2, 8);
      }
    }
  },
  mixins: [searchMixin]
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
