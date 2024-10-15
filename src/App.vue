<script>
import axios from './axiosConfig';
import UserInfo from './components/UserInfo.vue';
import UserForm from './components/UserForm.vue';

export default {
  name: 'App',
  data() {
    return {
      users: null,
      activeUserId: null,
      filterUserId: ''
    }
  },
  components: {
    UserInfo,
    UserForm
  },
  created() {
    this.loadUsers();
  },
  methods: {
    async loadUsers() {
      try {
        const response = await axios.get('/users', {
          params: this.filterUserId ? { id: this.filterUserId } : {}
        });
        this.users = response.data;
      } catch (error) {
        console.error('Error loading users:', error);
      }
    },
    setActiveUser(id) {
      this.activeUserId = id;
    },
    applyFilter() {
      this.loadUsers();
    },
    async createUser(newUser) {
      try {
        const response = await axios.post('/users', newUser);
        alert(`User created: ${JSON.stringify(response.data)}`);
      } catch (error) {
        console.error('Error creating user:', error);
      }
    }
  },
}
</script>

<template>
  <div>
    <input v-model="filterUserId" placeholder="Filter by UserId">
    <button @click="applyFilter">Apply Filter</button>

    <table v-if="users">
      <tbody>
        <tr v-for="user in users" :key="user.id">
          <td>{{ user.id }}</td>
          <td>{{ user.name }}</td>
          <td>{{ user.email }}</td>
          <td>{{ user.phone }}</td>
          <td>
            <button @click="() => setActiveUser(user.id)">Show details</button>
          </td>
        </tr>
      </tbody>
    </table>

    <UserInfo v-if="activeUserId" :userId="activeUserId" />
    <UserForm @submit="createUser" />
  </div>
</template>

<style scoped></style>