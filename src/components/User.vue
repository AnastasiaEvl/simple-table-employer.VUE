<script>

export default {
  props: {
    user: {
      type: Object,
      required: true
    },
    index: {
      type: Number,
      required: true
    },
    deleteUser: {
      type: Function,
      required: true
    }
  }
}
</script>

<template>
  <tr>
    <td>{{ index + 1 }}</td>
    <td>{{ user.name }}</td>
    <td>{{ user.surname }}</td>
    <td> {{ user.department }}</td>
    <td> {{ user.email }}</td>
    <td><button @click="deleteUser(index)" class="delete-btn">X</button></td>
  </tr>


</template>

<style scoped>

td {
  border: 1px solid #dddddd;
  padding: 5px;
}
.delete-btn{
  position: relative;
  height: 100%;
  width: 100%;
  transition: 0.6s;
}
.delete-btn:hover{
  transition: 0.6s;
  cursor: pointer;
  background-color: #ff7b5a;
  color:white;
  border-color: white;
}

</style>
