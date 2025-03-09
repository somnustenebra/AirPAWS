<template>
  <div id="capstone-app">
    <div id="nav">
      <!-- <router-link v-bind:to="{ name: 'home' }">Home</router-link>&nbsp;|&nbsp; -->

      <router-link v-if="$store.state.token !== '' && $route.name !=='home'" v-bind:to="{ name: 'home' }" style="color: white;">Home</router-link>
      <span v-if="$store.state.token !== ''" style="color: white;">&nbsp;|&nbsp;</span>
      <router-link v-bind:to="{ name: 'logout' }" v-if="$store.state.token != ''">Logout</router-link>
    </div>
    <router-view />
  </div>
</template>
