<template>
  <div>
    <h1>User Profile Dashboard</h1>

    <div>
      <img :src="user.profilePicture" alt="Profile Picture" style="width: 100px; height: 100px; border-radius: 50%;">
      <p><strong>Name:</strong> {{ user.name }}</p>
      <p><strong>Email:</strong> {{ user.email }}</p>
      <p><strong>Role:</strong> {{ user.isAdmin ? 'Admin' : 'Regular User' }}</p>
      <p><strong>Greeting:</strong> {{ greetingMessage }}</p>
      <p><strong>Age:</strong> {{ userAge }}</p>
    </div>

    <form @submit.prevent="updateUserProfile">
      <label for="name">Name:</label>
      <input v-model="user.name" type="text" id="name" required>

      <label for="email">Email:</label>
      <input v-model="user.email" type="email" id="email" required>

      <label for="profilePicture">Profile Picture URL:</label>
      <input v-model="user.profilePicture" type="text" id="profilePicture">

      <label for="isAdmin">Admin:</label>
      <input v-model="user.isAdmin" type="checkbox" id="isAdmin">

      <label for="birthdate">Birthdate:</label>
      <input v-model="user.birthdate" type="date" id="birthdate">

      <button type="submit">Update Profile</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      user: {
        name: 'John Doe',
        email: 'john.doe@example.com',
        profilePicture: 'https://placekitten.com/100/100', 
        isAdmin: false,
        birthdate: '1990-01-01',
      },
    };
  },
  computed: {
    greetingMessage() {
      return this.user.isAdmin ? 'Hello Admin!' : 'Welcome User!';
    },
    userAge() {
      const birthdate = new Date(this.user.birthdate);
      const today = new Date();
      const age = today.getFullYear() - birthdate.getFullYear();
      return age;
    },
  },
  methods: {
    updateUserProfile() {
      console.log('User profile updated!', this.user);
    },
  },
  watch: {
    user: {
      handler(newValue, oldValue) {
        console.log('User details modified!');
      },
      deep: true,
    },
  },
  created() {
    console.log('User profile component created!');
  },
};
</script>

<style scoped>
</style>
