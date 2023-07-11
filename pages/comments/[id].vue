<template>
  <button class="mui-button" @click="navigateTo('/')">Go back</button>
  <div class="card">
    <p class="mui-page">User id: {{ comment.id }}</p>
    <p class="mui-page">User name: {{ comment.name }}</p>
    <p class="mui-page">User email: {{ comment.email }}</p>
    <p class="mui-page">Comment id: {{ comment.postId }}</p>
    <p class="mui-page">Comment text: {{ comment.body }}</p>
  </div>
</template>

<script setup>
import axios from 'axios';

let baseApi = 'https://jsonplaceholder.typicode.com/comments'
let route = useRoute();
let comment = ref({});

const getComment = async() => {
  await axios
    .get(`${baseApi}/?id=${route.params.id}`)
    .then((res) => {
      comment.value = res.data[0]
      console.log(comment.value)
    })
  }
getComment();

</script>

<style>
.card{
  width: 500px;
  margin: 20px;
  border-radius: 4px;
  background-color: gainsboro;
  padding: 10px;
}

</style>
