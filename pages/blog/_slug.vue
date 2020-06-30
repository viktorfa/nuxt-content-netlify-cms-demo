<template>
  <div class="article">
    <nuxt-content :document="blogPost" />
  </div>
</template>

<script>
export default {
  async asyncData({ $content, params, error }) {
    const slug = "blog/" + params.slug; // path to the correct markdown file in the content folder
    const blogPost = await $content(slug)
      .fetch()
      .catch(err => {
        error({ statusCode: 404, message: "Page not found" });
      });
    return { blogPost };
  }
};
</script>

<style></style>
