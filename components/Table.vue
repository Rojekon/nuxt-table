<template>
    <table class="table">
      <thead>
        <tr>
          <th @click="sortById" style="cursor: pointer;">ID</th>
          <th>Name</th>
          <th>Email</th>
        </tr>
      </thead>
      <tbody>
          <tr v-for="comment in data[currPage-1]" :key="comment.id" @click="navigateTo(`/comments/${comment.id}`)">
              <td>{{ comment.id }}</td>
              <td>{{ comment.name }}</td>
              <td>{{ comment.email }}</td>
            </tr>
      </tbody>
    </table>
</template>
<script setup>


let sorted = ref(false);

const sortById = () => {
  if (sorted.value == true) {
    props.data[props.currPage-1].sort((a, b) => (a.id < b.id ? -1 : 1));
    sorted.value = false;
  } else {
    props.data[props.currPage-1].sort((a, b) => (a.id > b.id ? -1 : 1));
    sorted.value = true;
  }
};


const props = defineProps ({
    data: {
        type: Array,
        required: true
    },
    currPage: {
        type: Number,
        required: true
    }
})
</script>

<style>
.table {
  width: 100%;
  border-collapse: collapse;
  font-family: 'Roboto', sans-serif;
}

.table thead th {
  background-color: #2196f3;
  color: #ffffff;
  font-weight: bold;
  padding: 10px;
  text-align: left;
}

.table tbody td {
    cursor: pointer;
  padding: 10px;
  font-family: 'Roboto', sans-serif;
  border-bottom: 1px solid #ddd;
  font-size: 18px;
}

.table tbody tr:nth-child(even) {
  background-color: #f9f9f9;
}

.table tbody tr:nth-child(odd) {
  background-color: #fff;
}

.table tbody tr:hover {
  background-color: #e0e0e0;
}
</style>
