<template>
  <tr v-for="user in users" :key="user.id">
    <td>{{ user.id }}</td>
    <td>{{ user.name }}</td>
    <td>
      <img src="@/assets/email.svg" alt="" class="table__sortIcon">
      {{ user.email }}
    </td>
    <td>
      <img src="@/assets/telephone.svg" alt="" class="table__sortIcon">
      {{ user.phone }}
    </td>
    <td>{{ user.website }}</td>
  </tr>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: ['users']
}
</script>

<style scoped>

td {
  border-left: 1px solid #ECF0F1;
  border-right: 1px solid #ECF0F1;
  padding: 10px;
}

th {
  background-color: #4ECDC4;
}

tr:nth-of-type(even) td {
  background-color: #4ecdc447;
}
</style>