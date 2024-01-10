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
import axios from 'axios';
export default {
    name: "student",
    data() {
        return {
            students: {},
            isLoading:true,
        }
    },
    mounted() {
        this.getStudents();
        //
    },
    methods: {
        getStudents() {
            this.isLoading = true;
            axios.get(`http://localhost:8000/api/students`).then(res => {
                this.isLoading = false;
                this.students = res.data.students;
            });
        },
        deleteStudent(event, studentId) {
            if (confirm('Are you sure, that you want to delete this data? ')) {
                event.target.innerText = "Deleting";
                axios.delete(`http://localhost:8000/api/students/${studentId}/delete`).then(res => { 
                    event.target.innertText = "Delete";
                    this.getStudents();
                });
            }
        }
    }
}
</script>

<style>

</style>