<template>
  <Layout>
    <div class="post-title py-6 px-0 text-center">
      <h1 class="post-title__text transition duration-700 text-title-color">
        {{ $page.post.title }}
      </h1>

      <PostMeta :post="$page.post" />
    </div>
    <!-- TODO -->

    <div
      class="content-box max-w-screen-md my-0 mx-auto transition duration-700 bg-brand-color p-12 rounded-md shadow-md transition duration-700 text-body-color"
    >
      <div class="post">
        <div
          class="post__header w-24 -ml-10 -mt-10 mb-6 overflow-hidden rounded-t-md"
        >
          <g-image
            class="w-full"
            alt="Cover image"
            v-if="$page.post.cover_image"
            :src="$page.post.cover_image"
          />
        </div>

        <div
          class="markdown-body mb-8 text-body-color"
          v-html="$page.post.content"
        />

        <div class="post__footer">
          <PostTags :post="$page.post" />
        </div>
      </div>
    </div>

    <div class="post-comments p-6">
      <!-- Add comment widgets here -->
    </div>

    <Author class="post-author mt-6" />
  </Layout>
</template>

<script>
import PostMeta from '~/components/PostMeta';
import PostTags from '~/components/PostTags';
import Author from '~/components/Author.vue';

export default {
  components: {
    Author,
    PostMeta,
    PostTags
  },
  metaInfo() {
    return {
      title: this.$page.post.title,
      meta: [
        {
          name: 'description',
          content: this.$page.post.description
        }
      ]
    };
  }
};
</script>

<page-query>
  query Post($id: ID!) {
    post: post(id: $id) {
      title
      path
      date(format: "D. MMMM YYYY")
      timeToRead
      tags {
        id
        title
        path
      }
      description
      content
      cover_image(width: 860, blur: 10)
    }
  }
</page-query>

<style src="~/assets/css/github-markdown.css" />
