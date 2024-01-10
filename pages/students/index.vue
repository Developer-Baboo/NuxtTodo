<template>
  <div class="container mt-5">
    <div class="card">
        <div class="card-header">
            <h4>Student Lists
                <NuxtLink to="/students/create" class="btn btn-primary float-end">Add Student</NuxtLink>
            </h4>
        </div>
        <div class="card-body">
            <div v-if="isLoading" >
                    <Loading title="Loading..."/>
            </div>
            <div v-else>
                <table class="table table-striped table-bordered">
                    <thead>
                        <tr>
                            <th>ID</th>
                            <th>NAME</th>
                            <th>EMAIL</th>
                            <th>COURSE</th>
                            <th>Phone</th>
                            <th>ACTION</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(student, index) in students" :key="index">
                            <td>{{ student.id }}</td>
                            <td>{{ student.name }}</td>
                            <td>{{ student.email }}</td>
                            <td>{{ student.course }}</td>
                            <td>{{ student.phone }}</td>
                            <td>
                                <NuxtLink :to="`/students/${student.id}`" class="btn btn-success btn-sm mx-2">Edit</NuxtLink>
                                <button type="button" @click="deleteStudent($event, student.id)" class="btn btn-danger btn-sm mx-2" >Delete</button>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>
  </div>
</template>

<script>
// Importing a tool called axios for making HTTP requests
import axios from 'axios';

// Defining a new component called 'student'
export default {
    // The name of the component
    name: "student",

    // Data function returning initial data for the component
    data() {
        return {
            // Object to store a list of students
            students: {},
            // Boolean flag for loading state
            isLoading: true,
        }
    },

    // Lifecycle hook: mounted is called after the component has been added to the DOM
    mounted() {
        // Call the getStudents method to fetch student data when the component is mounted
        this.getStudents();
    },

    // Methods defined for the component
    methods: {
        // Method to fetch a list of students using an HTTP GET request
        getStudents() {
            // Set isLoading to true to show loading state
            this.isLoading = true;

            // Make a GET request to the specified API endpoint
            axios.get(`http://localhost:8000/api/students`).then(res => {
                // Once the data is fetched, set isLoading to false and update the students object
                this.isLoading = false;
                this.students = res.data.students;
            });
        },

        // Method to delete a student using an HTTP DELETE request
        deleteStudent(event, studentId) {
            // Ask for confirmation before deleting
            if (confirm('Are you sure you want to delete this data?')) {
                // Change the button text to indicate deletion is in progress
                event.target.innerText = "Deleting";

                // Make a DELETE request to delete the student data
                axios.delete(`http://localhost:8000/api/students/${studentId}/delete`).then(res => {
                    // Once deletion is successful, change the button text back and update the student list
                    event.target.innerText = "Delete";
                    this.getStudents();
                });
            }
        }
    }
}
</script>


<style>

</style>