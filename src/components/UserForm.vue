<script>
export default {
  name: 'UserForm',
  data() {
    return {
      email: '',
      name: '',
      phone: ''
    }
  },
  emits: ['submit'],
  methods: {
    handleSubmit() {
      this.$emit('submit', {
        email: this.email,
        name: this.name,
        phone: this.phone
      });
    }
  }
}
</script>

<template>
  <div class="container">
    <label for="email">Email</label>
    <input id="email" v-model="email">
    
    <label for="name">Name</label>
    <input id="name" v-model="name">
    
    <label for="phone">Phone</label>
    <input id="phone" v-model="phone">
    
    <button @click="handleSubmit">Save</button>
  </div>
</template>

<style scoped></style>