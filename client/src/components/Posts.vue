<template>
  <div class="posts">
    <h1>Posts</h1>
    <div v-if="posts.length > 0" class="table-wrap">
      <div>
        <router-link :to="{ name: 'NewPost' }" class="">Add Post</router-link>
      </div>
      <table>
        <tr>
          <td>Title</td>
          <td width="550">Description</td>
          <td width="100" align="center">Action</td>
        </tr>
        <tr v-for="post in posts" :key="post._id">
          <td>{{ post.title }}</td>
          <td>{{ post.description }}</td>
          <td align="center">
            <router-link :to="{ name: 'EditPost', params: {id: post._id } }">Edit</router-link>
            <a href="#">Delete</a>
          </td>
        </tr>
      </table>
    </div>
    <div v-else>
      There are no posts... Lets add one now <br> <br>
      <router-link :to="{name: 'NewPost'}" class="add_post_link">Add Post</router-link>
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
      this.posts = response.data.posts
    }
  }
}
</script>

<style>
.table-wrap {
  width:60%;
  margin: 0 auto;
  text-align: center;
}
table th, table tr {
  text-align: left;
}
table thead {
  background: #f2f2f2;
}
table tr td {
  padding: 10px;
}
table tr:nth-child(odd), table tr:nth-child(odd) a {
  background: #4d7ef7;
  color: #fff;
}
a{
  color:#4d7ef7;
}
.add_post_link{
  background: #4d7ef7;
  color: #ffffff;
  padding: 10px 80px;
  text-transform: uppercase;
  font-size: 12px;
  font-weight: bold;
}
</style>
