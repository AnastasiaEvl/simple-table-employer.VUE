<script>
import User from "@/components/User.vue";

export default {
  components: {User},
  data() {
    return {
      users: [],
      error: '',
      userName: '',
      userSurname: '',
      userDepartment: '',
      userEmail: ''
    }
  },
  mounted(){
    if(localStorage.users){
      this.users= localStorage.users
    }
  },
  methods: {
    sendData() {
      if (this.userName === '') {
        this.error = 'Name is empty'
        return
      } else if (this.userSurname === '') {
        this.error = 'Surname is empty'
        return
      } else if (this.userDepartment === '') {
        this.error = 'Department is empty'
        return
      } else if (this.userEmail === '') {
        this.error = 'Email is empty'
        return
      }
      this.error = ''
      if (this.users.length === 0) {
        this.users.push({
          name: this.userName,
          surname: this.userSurname,
          department: this.userDepartment,
          email: this.userEmail
        })
        this.userName = ''
        this.userSurname = ''
        this.userDepartment = ''
        this.userEmail = ''
      } else {
        if (this.users.find(el => el.email === this.userEmail)) {
          this.error = 'Already exist'
        } else {
          this.users.push({
            name: this.userName,
            surname: this.userSurname,
            department: this.userDepartment,
            email: this.userEmail
          })
        }
      }
      this.userName = ''
      this.userSurname = ''
      this.userDepartment = ''
      this.userEmail = ''
    },
    deleteUser(index) {
      this.users.splice(index, 1)
    }
  }
}

</script>

<template>
  <h2 class="title">List of employers</h2>
  <form class="task-form">
    <fieldset class="border-form">
      <input type="text" v-model="userName" placeholder="Name" class="input">
      <input type="text" v-model="userSurname" placeholder="Surname" class="input">
      <select v-model="userDepartment" class="input">
        <option disabled value="">Department</option>
        <option>Purchasing</option>
        <option>IT</option>
        <option>Sales</option>
        <option>Marketing</option>
      </select>
      <input type="email" v-model="userEmail" placeholder="Email" class="input">
    </fieldset>
  </form>
  <p class="error">{{ error }}</p>
  <button @click="sendData()" class="submit-btn">Add</button>
  <div v-if="users.length === 0" class="text-container">
    <p>List is empty!</p>
  </div>
  <table v-if="users.length !==0" class="table">
    <tr>
      <th>№</th>
      <th>Name</th>
      <th>Surname</th>
      <th>Department</th>
      <th>Email</th>
    </tr>
    <User v-for="(el, index) in users" :key="index" :user="el" :index="index" :deleteUser="deleteUser"/>
  </table>
</template>

<style scoped>
.title {
  text-align: center;
  color: white;
  padding-top: 2rem;
}
.task-form {
  margin: 3rem auto;
  width: 80%;
  padding: 2rem;
  display: flex;
  background-color: #5e83ba;
  justify-content: center;
}

.input {
  margin-right: 1rem;
  padding: 0.5rem;
  text-align: center;
}

.submit-btn {
  color: white;
  background-color: #091d36;
  padding: 1rem 10rem;
  border-radius: 0.5rem;
  transition: 0.6s;
  margin: 0 auto;
  display: block;
}

.submit-btn:hover {
  background-color: #394e79;
  cursor: pointer;
  transition: 0.6s;
}

.text-container {
  text-align: center;
  padding-top: 3rem;
}

h3 {
  font-weight: lighter;
}

.error {
  color: red;
  text-align: center;
}

.table {
  width: 100%;
  margin-bottom: 20px;
  border: 1px solid #dddddd;
  border-collapse: collapse;
  margin-top: 2rem;
}

.table th {
  font-weight: bold;
  padding: 5px;
  background: #efefef;
  border: 1px solid #dddddd;
}

.table td {
  border: 1px solid #dddddd;
  padding: 5px;
}
.border-form {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 1rem;
}
</style>
