<template>
  <div class="container mt-5">
    <div class="card">
        <div class="card-header">
            <h4>Student Lists
                <NuxtLink to="/students/create" class="btn btn-primary float-end">Add Student</NuxtLink>
            </h4>
        </div>
        <div class="card-body">
            <table class="table table-striped table-bordered">
                <thead>
                    <tr>
                        <th>ID</th>
                        <th>NAME</th>
                        <th>EMAIL</th>
                        <th>COURSE</th>
                        <th>Phone</th>
                        <th>CREATED AT</th>
                        <th>UPDATED AT</th>
                        <th>ACTION</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(student, index) in students" :key="index">
                        <td>{{student.id}}</td>
                        <td>{{ student.name }}</td>
                        <td>{{ student.email }}</td>
                        <td>{{ student.course }}</td>
                        <td>{{ student.phone }}</td>
                        <td>{{ student.created_at }}</td>
                        <td>{{ student.updated_at }}</td>
                        <td><button class="btn btn-danger btn-sm" >Delete</button></td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
    name: "student",
    data() {
        return {
            students:{},
        }
    },
    mounted() {
        this.getStudents();
        //
    },
    methods: {
        getStudents() {
            axios.get(`http://localhost:8000/api/students`).then(res => {
                this.students = res.data.students;
            });
        }
    }

}
</script>

<style>

</style>