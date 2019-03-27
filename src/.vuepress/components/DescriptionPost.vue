<template>
  <div>
    <p>{{date}} • {{name}}</p>
  </div>
</template>

<script>
export default {
  computed: {
    name: function() {
      return this.$page.frontmatter.autor;
    },
    date: function() {
      return this.$page.frontmatter.date;
    },
    doneIn: function(){
      let numberCharacters = this.$page.frontmatter.nc || 0;
      const wordsPerMinute = 200; // It's a average case
      return Math.ceil(numberCharacters / wordsPerMinute);
    }
  }
};
</script>

<style scoped>
p {
  font-size: 0.9em;
}
</style>
