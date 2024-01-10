<template>
  <div>
    <h1>Table Post</h1>
    <div v-if="comments.length">
        <h2>Comments:</h2>
        <ul>
          <li v-for="comment in comments" :key="comment.id">
            <strong>{{ comment.title }}</strong>: {{ comment.body }}
          </li>
        </ul>
      </div>
    <table border="1">
      <tr>
      <td>Id</td>
      <td>Title</td>
      <td>Body</td>
      <td>UserId</td>
      <td>Action</td>
      </tr>
      <tr v-for="item in posts" :key="item.id">
        <td>{{ item.id }}</td>
        <td>{{ item.title }}</td>
        <td>{{ item.body }}</td>
        <td>{{ item.userId}}</td>
        <td>
          <button @click="loadComments(item.id)" class="btn btn-primary">
              View Comments
            </button>
        </td>
      </tr>
    </table>
  </div>
</template>
<script>
import axios from 'axios';
export default {
  name: "TablePost",
  data() {
    return {
      posts: [],
      comments: [],
    }
  },
  async mounted() {
    let result = await axios.get("https://dummyjson.com/posts");
    console.warn(result)
    this.posts = result.data.posts
  },
  methods: {
    async loadComments(id) {
    const result = await axios.get(`https://dummyjson.com/posts/${id}/comments`);
    console.warn(result)
          this.comments = result.data.comments;
         
      },
  }
}
</script>

<style>
td{
  width: 220px;
}

h1{
  text-align: center;
}
</style>
