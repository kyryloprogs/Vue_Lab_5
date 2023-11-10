<template>
    <div>
      <h1>Сторінка "Login"</h1>
      <form @submit="login">
        <label for="email">Email:</label>
        <input type="email" id="email" v-model="email" required />
        <label for="password">Password:</label>
        <input type="password" id="password" v-model="password" required />
        <button type="submit">Login</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        email: '',
        password: '',
      };
    },
    methods: {
      async login() {
        try {
          await this.$fire.auth.signInWithEmailAndPassword(this.email, this.password);
          this.$router.push('/todo');
        } catch (error) {
          console.error(error);
        }
      },
    },
  };