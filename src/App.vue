<script setup lang="ts">
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <div>
    <a target="_blank">
      <img src="/NDID.png" class="logo" alt="NDID logo" />
    </a>
    <a target="_blank">
      <img src="./assets/Finnomena.jpg" class="logo vue" alt="Finnomena logo" />
    </a>
  </div>
  <HelloWorld msg="NDID x Finnomena" />
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
