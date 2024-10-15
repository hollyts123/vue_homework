<script>
import axios from '../axiosConfig';

export default {
  name: 'UserInfo',
  props: {
    userId: {
      type: Number,
      required: true
    }
  },
  data() {
    return {
      user: null,
      error: null
    }
  },
  methods: {
    async loadUser() {
      try {
        const response = await axios.get(`/users/${this.userId}`);
        this.user = response.data;
      } catch (error) {
        this.error = 'Error loading user';
      }
    }
  },
  watch: {
    userId() {
      this.loadUser();
    }
  },
  created() {
    this.loadUser();
  }
}
</script>

<template>
  <div v-if="user">
    <h3>User Details</h3>
    <p>{{ user.name }}</p>
    <p>{{ user.email }}</p>
    <p>{{ user.phone }}</p>
  </div>
  <div v-else-if="error">
    <p>{{ error }}</p>
  </div>
  <div v-else>
    Loading...
  </div>
</template>

<style scoped></style>