# Authenticating Vuepress Apps with Auth0

## Project setup

1. Clone the project
2. Run `yarn`
3. Create a file `auth_config.js` inside `/src/.vuepress/auth`

```javascript
const config = {
  domain: "YOUR_AUTH0_DOMAIN",
  clientId: "YOUR_CLIENT_ID"
};

export default config;
```

4. Replace the placeholders with your respective [Auth0](https://auth0.com) credentials (Please ensure that the auth0 client application is of type ‘Single Page Applications’)
5. Run `yarn dev` to launch the application
