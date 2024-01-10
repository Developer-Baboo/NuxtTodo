<template>
  <div>
    <div class="container mt-5">
      <form>
        <h1 class="text-center mb-4" style="color: #e74c3c;">Contact Us</h1>
        <div class="mb-3">
          <label for="name" class="form-label" style="color: #3498db;">Your Name</label>
          <input type="text" class="form-control" id="name" placeholder="Enter your name">
        </div>
        <div class="mb-3">
          <label for="email" class="form-label" style="color: #3498db;">Email Address</label>
          <input type="email" class="form-control" id="email" placeholder="Enter your email">
        </div>
        <div class="mb-3">
          <label for="message" class="form-label" style="color: #3498db;">Your Message</label>
          <textarea class="form-control" id="message" rows="5" placeholder="Enter your message"></textarea>
        </div>
        <button type="submit" class="btn btn-primary"
          style="background-color: #e74c3c; border-color: #e74c3c;">Submit</button>
      </form>
    </div>
  </div>
</template>

<script setup lang="ts"></script>

<style scoped>
/* Add your custom styles here */
form {
  max-width: 600px;
  margin: 0 auto;
}

h1 {
  font-size: 2rem;
}

/* Add more styles as needed */
</style>
