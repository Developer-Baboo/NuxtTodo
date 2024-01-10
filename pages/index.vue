<template>
  <div class="container mt-5">
    <center>
      <h1 class="text-primary">Welcome to My NuxtJs Todo App <i class="fas fa-hand-wave"></i></h1>
    </center>
    <center>
      <p>This is a dummy content for the home page. You can customize and add more content here.</p>
    </center>

    <div class="row mt-4">
      <div class="col-md-6">
        <div class="card ">
          <div class="card-body">
            <h5 class="card-title text-warning">Feature 1</h5>
            <p class="card-text">Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin dapibus quam in ex varius,
              ac finibus quam efficitur.</p>
            <button class="btn btn-warning">Learn More</button>
            <i class="bi bi-alarm-fill animate__animated animate__bounce animate__infinite"></i>
          </div>
        </div>
      </div>

      <div class="col-md-6">
        <div class="card">
          <div class="card-body">
            <h5 class="card-title text-info">Feature 2</h5>
            <p class="card-text">Sed ullamcorper, lacus sed dapibus convallis, felis orci ullamcorper ex, eu bibendum
              mauris urna eu velit.</p>
            <button class="btn btn-info">Explore</button>
            <i class="bi bi-check2-circle animate__animated animate__pulse animate__infinite"></i>
          </div>
        </div>
      </div>
    </div>
    <div class="row mt-4">
        <div class="col-md-6">
          <div class="card">
            <div class="card-body">
              <h5 class="card-title text-danger">Feature 3</h5>
              <p class="card-text">Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin dapibus quam in ex varius,
                ac finibus quam efficitur.</p>
              <button class="btn btn-danger">Learn More</button>
              <i class="bi bi-alarm-fill animate__animated animate__bounce animate__infinite"></i>
            </div>
          </div>
        </div>

        <div class="col-md-6">
          <div class="card">
            <div class="card-body">
              <h5 class="card-title text-dark">Feature 4</h5>
              <p class="card-text">Sed ullamcorper, lacus sed dapibus convallis, felis orci ullamcorper ex, eu bibendum
                mauris urna eu velit.</p>
              <button class="btn btn-dark">Explore</button>
              <i class="bi bi-check2-circle animate__animated animate__pulse animate__infinite"></i>
            </div>
          </div>
        </div>
      </div>
  </div>
</template>

<script setup>
</script>

<style scoped>
/* Add your custom styles here */
/* Example animations using animate.css */
@import url('https://cdn.jsdelivr.net/npm/animate.css');

/* Override Bootstrap colors if needed */
.text-primary {
  color: #007BFF !important;
}

.text-success {
  color: #28A745 !important;
}

.text-info {
  color: #17A2B8 !important;
}

.btn-warning {
  background-color: #FFC107 !important;
  border-color: #FFC107 !important;
}

.btn-danger {
  background-color: #DC3545 !important;
  border-color: #DC3545 !important;
}
</style>


<script setup lang="ts">
import { useHead } from "nuxt/app";
    useHead({
        title: 'Home Page',
    })
</script>