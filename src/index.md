---
home: true
footer: Made by Auth0 User with ❤️
---

<template>
  <div class="main-content">
    <div v-if="user">
      <p align="center">
        Hi {{user.given_name}} {{user.family_name}}, Welcome to the Vuepress Blog
      </p>
      <p align="center">
        <LogoutButton :client="auth0client" />
      </p>
    </div>
    <div v-else>
      <p align="center">
        You are currently not logged-in to the Application. Please use the login button below to sign in
      </p>
      <p align="center">
        <LoginButton :client="auth0client" @login-complete="getUser()" />
      </p>
    </div>
  </div>
  
  
</template>

<script>
import auth from "./.vuepress/auth";
import LoginButton from "./.vuepress/components/LoginButton";
import LogoutButton from "./.vuepress/components/LogoutButton";


export default {
  data() {
    return {
      
      auth0client : null,
      loginButton: null,
      user : null
    }
  },

  async mounted(){
    this.auth0client = await auth.createClient();
    console.log(this.auth0client);

    this.user = await this.auth0client.getUser();
    console.log(this.user);
    
  },

  methods : {
    async login () {
      await auth.loginWithPopup(this.auth0client);
    },
    async getUser(){
      this.user = await this.auth0client.getUser();
      console.log(this.user);
    }
  }
}
</script>

<style>
.main-content{
  text-align: "center"
}
</style>
