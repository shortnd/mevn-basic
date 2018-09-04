<template>
  <div class="posts">
    <h1>Posts</h1>
    This file will list all the posts

    <div v-for="(post, index) in posts" :key="index">
      <p>
        <span><b>{{ post.title }}</b></span>
        <span>{{ post.description }}</span>
      </p>
    </div>
  </div>
</template>

<script>
import PostsServices from '@/services/PostsServices'
export default {
  name: 'posts',
  data () {
    return {
      posts: []
    }
  },
  mounted () {
    this.getPosts()
  },
  methods: {
    async getPosts () {
      const response = await PostsServices.fetchPosts()
      this.posts = response.data
    }
  }
}
</script>

<style>

</style>
