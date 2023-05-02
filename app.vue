<template>
  <div>
    <h1>Bug Example</h1>
    <button @click="onLogin">Login</button>
  </div>
</template>
<script setup>
import { handleIncomingRedirect, login, getDefaultSession } from '@inrupt/solid-client-authn-browser'

async function onLogin() {
  console.log('handleIncomingRedirect...')
  await handleIncomingRedirect()
  console.log('getDefaultSession:', getDefaultSession())
  if (!getDefaultSession().info.isLoggedIn) {
    console.log('login...')
    await login({
      oidcIssuer: "https://login.inrupt.com",
      redirectUrl: window.location.href,
      clientName: "Contracts"
    })
  }
}

</script>
