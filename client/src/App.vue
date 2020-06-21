<template>
  <div id="app">
    <form action="">
      <input type="text" name="email" id="email" v-model="email" />
      <br />
      <input type="text" name="password" id="password" v-model="password" />
      <br />
      <button type="submit" @click.prevent="login">Login</button>
    </form>
  </div>
</template>

<script>
import axios from 'axios';

const apiBase = 'http://localhost:8000';

export default {
  data: () => {
    return {
      email: 'alaminfirdows@gmail.com',
      password: 'alaminfirdows',
      isAuthenticated: true
    };
  },
  methods: {
    async login() {
      await axios.get(`${apiBase}/sanctum/csrf-cookie`);

      //   await axios
      //     .post(`${apiBase}/login`, {
      //       email: this.email,
      //       password: this.password
      //     })
      //     .then(() => {
      //       this.isAuthenticated = true;
      //     });
      if (this.isAuthenticated) {
        await axios.get(`${apiBase}/api/user`, { withCredentials: true }).then(response => {
          console.log(response);
        });
      } else {
        console.log('Un authenticated');
      }
    }
  }
};
</script>
