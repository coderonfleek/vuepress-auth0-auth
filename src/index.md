---
home: true
heroImage: https://v1.vuepress.vuejs.org/hero.png
tagline: A sample App for Authentication with Auth0
actionText: Quick Start →
actionLink: /guide/
features:
  - title: Feature 1 Title
    details: Feature 1 Description
  - title: Feature 2 Title
    details: Feature 2 Description
  - title: Feature 3 Title
    details: Feature 3 Description
footer: Made by Fikayo Adepoju with ❤️
---

## Getting Started

{{message}}

<p v-if="user">{{user.given_name}} {{user.family_name}}</p>

<template>
  <LoginButton v-if="!user" :client="auth0client" @login-complete="getUser()" />
  <LogoutButton v-else :client="auth0client" />
</template>

<script>
import auth from "./.vuepress/auth";
import LoginButton from "./.vuepress/components/LoginButton";
import LogoutButton from "./.vuepress/components/LogoutButton";


export default {
  data() {
    return {
      message: "Hey, this is dynamic",
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
