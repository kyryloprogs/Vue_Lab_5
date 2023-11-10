<template>
    <div>
      <h1>Сторінка "Register"</h1>
      <form @submit="register">
        <label for="email">Email:</label>
        <input type="email" id="email" v-model="email" required />
        <label for="password">Password:</label>
        <input type="password" id="password" v-model="password" required />
        <button type="submit">Register</button>
      </form>
      <button @click="sendEmailVerification">Відправити лист для верифікації</button>
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
      async register() {
        try {
          const userCredential = await this.$fire.auth.createUserWithEmailAndPassword(this.email, this.password);
          const user = userCredential.user;
          await user.sendEmailVerification();
          this.$router.push('/login');
        } catch (error) {
          console.error(error);
   
        }
      },
      async sendEmailVerification() {
        try {
          const user = this.$fire.auth.currentUser;
          await user.sendEmailVerification();
        } catch (error) {
          console.error(error);
        }
      },
    },
  };
  </script>