<template>
  <div>
    <h1>Bug Example</h1>
    <button @click="onLogin">Login</button>
    <button @click="completeLogin">Finish login</button>
  </div>
</template>
<script setup>
import {
  handleIncomingRedirect,
  login,
  getDefaultSession,
  Session,
} from "@inrupt/solid-client-authn-browser";

const session = new Session();

async function onLogin() {
  if (!session.info.isLoggedIn) {
    console.log("login...");
    await session.login({
      oidcIssuer: "https://login.inrupt.com",
      redirectUrl: window.location.href,
      clientName: "Contracts",
    });
  }
}

async function completeLogin() {
  const info = await session.handleIncomingRedirect();
  console.debug(JSON.stringify(session.info));
}
</script>
