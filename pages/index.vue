<template>
  <Table :data="data" :currPage="page"></Table>
  <div class="container">
    <button class="mui-button" @click="previousPage" :disabled="page === 1">Previous</button>
    <p class="mui-page">{{ page }} out of {{ totalPages }}</p>
    <button class="mui-button" @click="nextPage" :disabled="page === totalPages">Next</button>
  </div>
</template>

<script setup>
import Table from "../components/Table.vue";
import axios from "axios";

let data = ref([]);
let page = ref(1);
let perPage = ref(10);
let totalPages = ref(0);
let pagination = ([]);
let baseApi = 'https://jsonplaceholder.typicode.com/comments'


const fetchComments = () => {
  let comments = []
  axios
    .get(baseApi)
    .then((res) => {
      comments = res.data;
      totalPages.value = comments.length / perPage.value;
      for(let i=0; i < comments.length;i+= +perPage.value){
        data.value.push(comments.slice(i,i+ +perPage.value));
      }
      for(let i=1; i<totalPages.value; i++){
        pagination.push(i);
      }
    });
};


const previousPage = () => {
  if (page.value > 1) {
    page.value--;
  }
};

const nextPage = () => {
  if (page.value < totalPages.value) {
    page.value++;
  }
};

onMounted(fetchComments);

</script>

<style>
.mui-button {
  background-color: #2196f3;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 18px;
  margin: 0 20px;
  font-family: 'Roboto', sans-serif;
}

.mui-button:disabled{
  background-color: #4a7496;
}

.mui-page {
  background-color: gray;
  border-radius: 4px;
  border: 1px solid gainsboro;
  font-size: 18px;
  color: white;
  margin: 10px 0;
  padding: 5px;
  font-family: 'Roboto', sans-serif;
}

.container {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 10px;
  width: 100%;
}
</style>
