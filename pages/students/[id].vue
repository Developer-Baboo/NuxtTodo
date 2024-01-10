<template>
  <div class="mt-5 container">
      <div class="card">
          <div class="card-header">
              <h4>Edit Student <NuxtLink to="/students" class="btn btn-danger float-end">Back</NuxtLink>
              </h4>
          </div>
          <div class="card-body">
              <!-- {{ this.errorList }} -->
              <div v-if="isLoading" >
                  <Loading :title="isLoadingTitle" />
              </div>
              <div v-else>
                  <form @submit.prevent="updateStudent">
                      <div class="mb-3">
                          <label for="">Name</label>
                          <input type="text" v-model="student.name" class="form-control">
                           <!-- Show an error message if there's an issue with the name input -->
                          <span class="text-danger" v-if="this.errorList.name">{{ this.errorList.name[0] }}</span>
                        
                      </div>
                      <div class="mb-3">
                          <label for="">Course</label>
                          <input type="text" v-model="student.course" class="form-control">
                           <!-- Show an error message if there's an issue with the course input -->
                          <span class="text-danger" v-if="this.errorList.course">{{ this.errorList.course[0] }}</span>
                      </div>
                      <div class="mb-3">
                          <label for="">Email</label>
                          <input type="text" v-model="student.email" class="form-control">
                           <!-- Show an error message if there's an issue with the email input -->
                          <span class="text-danger" v-if="this.errorList.email">{{ this.errorList.email[0] }}</span>
                      </div>
                      <div class="mb-3">
                          <label for="">Phone</label>
                          <input type="text" v-model="student.phone" class="form-control">
                           <!-- Show an error message if there's an issue with the phone input -->
                          <span class="text-danger" v-if="this.errorList.phone">{{ this.errorList.phone[0] }}</span>
                      </div>
                      <div class="mb-3">
                              <button type="submit" class="btn btn-primary" >Update</button>
                          </div>
                  </form>
              </div>
            
          </div>
      </div>
    </div>
</template>

<script>
// Importing a tool called axios for making HTTP requests
import axios from 'axios';

// Defining a new component called 'studentCreate'
export default {
  // The name of the component
  name: 'studentCreate',

  // Data function returning initial data for the component
  data() {
    return {
      // Initial value for studentId
      studentId: '',
      // Empty object to store student data
      student: {},
      // Boolean flag for loading state
      isLoading: false,
      // Loading title text
      isLoadingTitle: 'Loading',
      // Object to store validation errors
      errorList: {}
    }
  },

  // Lifecycle hook: mounted is called after the component has been added to the DOM
  mounted() {
    // Get the studentId from the route parameters
    this.studentId = this.$route.params.id

    // Call the getStudent method to fetch student data
    this.getStudent(this.studentId);
  },

  // Methods defined for the component
  methods: {
    // Method to fetch student data using an HTTP GET request
    getStudent(studentId) {
      // Set isLoading to true to show loading state
      this.isLoading = true;

      // Make a GET request to the specified API endpoint
      axios.get(`http://127.0.0.1:8000/api/students/${studentId}/edit`).then(res => {
        // Once the data is fetched, set isLoading to false and update the student object
        this.isLoading = false;
        this.student = res.data.student;
      });
    },

    // Method to update student data using an HTTP PUT request
    updateStudent() {
      // Set isLoading to true and update loading title
      this.isLoading = true;
      this.isLoadingTitle = "Updating....!";

      // Store the reference to 'this' in a variable for later use in the catch block
      var myThis = this;

      // Make a PUT request to update student data
      axios.put(`http://localhost:8000/api/students/${this.studentId}/edit`, this.student).then(res => {
        // Once the update is successful, log the response, show an alert, and reset loading state
        console.log(res, 'res');
        alert(res.data.message);
        this.isLoading = false;
        this.isLoadingTitle = 'Loading';

        // Clear any previous validation errors
        this.errorList = {};
      })
        .catch(function (error) {
          // If there's an error, log it and handle validation errors if status is 422
          console.log(error, 'errors');
          if (error.response) {
            if (error.response.status == 422) {
              myThis.errorList = error.response.data.errors;
            }
          }
          // Set isLoading to false to end the loading state
          myThis.isLoading = false;
        });
    }
  }
}
</script>

<style lang="scss" scoped>

</style>