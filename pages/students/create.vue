<template>
  <div class="mt-5 container">
    <div class="card">
        <div class="card-header">
            <h4>Add Student <NuxtLink to="/students" class="btn btn-danger float-end">Back</NuxtLink>
            </h4>
        </div>
        <div class="card-body">
            <!-- {{ this.errorList }} -->
            <div v-if="isLoading" >
                <Loading :title="isLoadingTitle" />
            </div>
            <div v-else>
                <form @submit.prevent="saveStudent">
                    <div class="mb-3">
                        <label for="">Name</label>
                        <input type="text" v-model="student.name" class="form-control">
                        <span class="text-danger" v-if="this.errorList.name">{{ this.errorList.name[0] }}</span>
                        
                    </div>
                    <div class="mb-3">
                        <label for="">Course</label>
                        <input type="text" v-model="student.course" class="form-control">
                        <span class="text-danger" v-if="this.errorList.course">{{ this.errorList.course[0] }}</span>
                    </div>
                    <div class="mb-3">
                        <label for="">Email</label>
                        <input type="text" v-model="student.email" class="form-control">
                        <span class="text-danger" v-if="this.errorList.email">{{this.errorList.email[0]}}</span>
                    </div>
                    <div class="mb-3">
                        <label for="">Phone</label>
                        <input type="text" v-model="student.phone" class="form-control">
                        <span class="text-danger" v-if="this.errorList.phone">{{ this.errorList.phone[0] }}</span>
                    </div>
                    <div class="mb-3">
                            <button type="submit" class="btn btn-primary" >Save</button>
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
            // Object to store student information with initial values
            student: {
                name: '',
                course: '',
                email: '',
                phone: '',
            },
            // Boolean flag for loading state
            isLoading: false,
            // Loading title text
            isLoadingTitle: 'Loading',
            // Object to store validation errors
            errorList: {}
        }
    },

    // Methods defined for the component
    methods: {
        // Method to save student data using an HTTP POST request
        saveStudent() {
            // Set isLoading to true and update loading title
            this.isLoading = true;
            this.isLoadingTitle = "Saving";

            // Store the reference to 'this' in a variable for later use in the catch block
            var myThis = this;

            // Make a POST request to save new student data
            axios.post(`http://localhost:8000/api/students`, this.student).then(res => {
                // Once the save is successful, log the response, show an alert, and reset loading state
                console.log(res, 'res');
                alert(res.data.message);

                // Clear input fields after successful save
                this.student.name = '';
                this.student.course = '';
                this.student.email = '';
                this.student.phone = '';

                this.isLoading = false;
                this.isLoadingTitle = 'Loading';

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

<style>

</style>