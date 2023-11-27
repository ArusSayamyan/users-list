<template>
  <div class="mainContainer">
    <div class="header">
      <label class="search__block">
        <img src="@/assets/search.svg" alt="" class="search">
        <input type="search" class="search__item" v-model="filter" @input="findUser($event)">
      </label>
      <button class="add__user" @click="addNewUser">
        Add new user
      </button>
    </div>
    <div class="table__content">
      <table class="table">
        <thead>
        <tr>
          <th>
            <img src="@/assets/sort-up.svg" alt="" class="table__sortIcon" @click="sortTableRows('id')">
            ID
          </th>
          <th>
            <img src="@/assets/sort-up.svg" alt="" class="table__sortIcon" @click="sortTableRows('name')">
            Name
          </th>
          <th>
            <img src="@/assets/sort-up.svg" alt="" class="table__sortIcon" @click="sortTableRows('email')">
            Email
          </th>
          <th>phone</th>
          <th>
            <img src="@/assets/sort-up.svg" alt="" class="table__sortIcon" @click="sortTableRows('website')">
            website
          </th>
        </tr>
        </thead>
        <tbody>
        <user-info :users="filteredUsers" v-if="isFiltered && filteredUsers.length > 0"></user-info>
        <user-info :users="users" v-else-if="!isFiltered"></user-info>
        <p v-else-if="filteredUsers.length === 0" class="info__message">No user found</p>
        </tbody>
      </table>

    </div>
  </div>

</template>

<script setup>
import UserInfo from "@/components/UserInfo.vue";
import {ref, computed} from "vue";

const users = ref();
const isFiltered = ref(false)
const formIsVisible = ref(false)
const filter = ref('')
async function getData() {
  const data = await fetch('https://jsonplaceholder.typicode.com/users');
  users.value = await data.json()

}

getData();

function sortTableRows(name) {
  users.value.sort(function (a, b) {
    if (a[name] < b[name]) {
      return -1;
    }
    if (a[name] > b[name]) {
      return 1;
    }
    return 0;
  });
}


function findUser() {
  isFiltered.value = true
}

const filteredUsers = computed(() => {
  return users.value.filter(user => user.name.toLowerCase().includes(filter.value.toLowerCase()))
})


// TODO
function addNewUser() {
  formIsVisible.value = true;
  console.log(formIsVisible.value)
}


</script>

<style scoped>
.mainContainer {
  max-width: 800px;
  width: 100%;
  margin: 0 auto;
}

table {
  width: 100%;
  border-collapse: collapse;
  text-align: left;
}

td, th {
  border-top: 1px solid #ECF0F1;
  padding: 10px;
}

th {
  background-color: #4ECDC4;
}

.search__item {
  outline: none;
  border: none;
  padding: 3px 5px;
  width: 100%;
  background: none;

}

.search__block {
  max-width: 300px;
  width: 100%;
  display: flex;
  justify-content: space-between;
  background-color: #4ecdc447;
  border-radius: 5px;
  padding: 5px;
}

.info__message {
  width: 100%;
  position: absolute;
  text-align: center;
  font-size: 25px;
  font-family: sans-serif;
}

.table__content {
  overflow-x: auto;
}

.header {
  display: flex;
  justify-content: space-between;
  margin-bottom: 25px;
}

.add__user {
  border: none;
  background: #4ecdc447;
  padding: 8px;
  border-radius: 5px;
}

.add__user:hover {
  background: unset;
  color: #4ECDC4;
  outline: 2px solid #4ECDC4;
}

</style>
