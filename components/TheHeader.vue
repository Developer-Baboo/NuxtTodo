<template>
  <div>
    <nav class="navbar navbar-expand-lg bg-body-tertiary shadow">
      <div class="container">
        <NuxtLink class="navbar-brand" to="/">Navbar</NuxtLink>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent"
          aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav ms-auto mb-2 mb-lg-0">
            <li class="nav-item">
              <NuxtLink class="nav-link " to="/">Home</NuxtLink>
            </li>
            <li class="nav-item">
              <NuxtLink class="nav-link" to="/students">Students</NuxtLink>
            </li>
            <li class="nav-item">
              <NuxtLink class="nav-link" to="/about-us">About Us</NuxtLink>
            </li>
            <li class="nav-item">
              <NuxtLink class="nav-link" to="/contact-us" >Contact Us</NuxtLink>
            </li>
          </ul>
        </div>
      </div>
    </nav>
  </div>
</template>

<script setup>
import { useRoute } from 'vue-router';

const isActive = (route) => {
  const currentRoute = useRoute();
  return currentRoute.path === route;
};
</script>

<style scoped>
/* Add your custom styles here */
.nav-link.active {
  color: #ffffff;
  /* Set the active link color */
}
</style>
