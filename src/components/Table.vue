<template>
    <div class="home">
      <h1>Hello {{ name }}, Welcome to the User Page</h1>
      <table>
        <tr>
          <td>Id#</td>
          <td>Name</td>
          <td>Email</td>
          <td>Created at</td>
          <td>Updated at</td>
          <!-- <td>Action</td> -->
        </tr>
        <tr v-for="user in users" :key="user._id">
          <td>{{ user._id }}</td>
          <td>{{ user.name }}</td>
          <td>{{ user.email }}</td>
          <td>{{ user.createdAt }}</td>
          <td>{{ user.updatedAt }}</td>
          <!-- <td>
            <button class="btn-trash" @click="deleteUser(user._id)">Delete</button>
          </td> -->
        </tr>
      </table>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue';
  import axios from 'axios';
  
  const name = 'User';
  const users = ref([]);
  
  const deleteUser = async (id) => {
    try {
      let result = await axios.delete(`./data/dummy.json/${id}`);
      if (result.status === 200) {
        loadData();
      }
    } catch (error) {
      console.error(error);
    }
  };
  
  const loadData = async () => {
    try {
      let result = await axios.get("./data/dummy.json");
      users.value = result.data.Users;
    } catch (error) {
      console.error(error);
    }
  };
  
  onMounted(() => {
    loadData();
  });
  </script>
  
  <style scoped>
  h1 {
    margin-top: 10px;
  }
  table {
    margin-left: auto;
    margin-right: auto;
    margin-top: 10px;
    border: 2px solid skyblue;
    border-collapse: collapse;
  }
  td {
    width: 160px;
    height: 40px;
    border: 2px solid skyblue;
    background: #eee;
    padding: 10px;
  }
  .btn-trash {
    border: 1px solid skyblue;
    padding: 5px;
    margin-left: 5px;
    background: crimson;
    color: white;
    text-decoration: none;
  }
  </style>
  