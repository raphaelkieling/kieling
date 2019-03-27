<template>
  <div>
    <div v-for="post in posts" class="card">
      <span class="card--description">{{post.frontmatter.date}} - {{post.frontmatter.autor}}</span>
      <router-link class="card--link" v-bind:to="post.path">{{post.title}}</router-link>
    </div>
  </div>
</template>


<script>
export default {
  mounted: function() {
    console.log(this.$site.pages);
  },
  computed: {
    posts() {
      return this.$site.pages
        .filter(page => !page.frontmatter.private)
        .filter(page => page.path.startsWith("/posts/"))
        .reverse();
    }
  }
};
</script>

<style scoped>
.card {
  display: flex;
  flex-direction: column;
  margin-bottom: 20px;
}

.card--description {
  font-size: 13px;
  color: gray;
}

.card--link {
  font-size: 1.4em;
  margin-top: 5px;
}
</style>
