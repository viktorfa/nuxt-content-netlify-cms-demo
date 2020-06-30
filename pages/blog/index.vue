<template>
  <div class="article">
    <div v-for="post in blogPosts" :key="post.slug">
      <div>
        <nuxt-link :to="post.path">
          <h2>{{ post.title }}</h2>
        </nuxt-link>
        <p class="text-gray-800 text-sm">
          {{ new Date(post.date).toLocaleDateString() }}
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ $content }) {
    const blogPosts = await $content("blog")
      .where({ draft: { $ne: true } })
      .fetch();
    return { blogPosts };
  }
};
</script>

<style></style>
