<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header class="container_head">
    <div class="top_nav">
      <RouterLink to="/" class="nav_a">Home</RouterLink>
    </div>
  </header>
  <RouterView />
</template>

<style scoped>
.container_head{
  text-align: -webkit-center;
}
.top_nav {
  background-color: #333;
  overflow: hidden;
  border-radius: 10px;
  margin-top: 15px;
  width: 75px;
}

a:hover {
  background-color: #ddd !important;
  color: black !important;
}

.nav_a {
  float: left;
  color: #f2f2f2;
  text-align: center;
  padding: 14px 16px;
  text-decoration: none;
  font-size: 17px;
}
</style>
