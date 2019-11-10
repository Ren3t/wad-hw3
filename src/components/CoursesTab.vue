<template>
    <div id="courses-container" v-show="show">
        <h1 class="title">Courses</h1>
        <table id="courses">
            <thead>
            <tr>
                <th>#</th>
                <th>Course Title</th>
                <th>Semester</th>
                <th>Grade</th>
            </tr>
            </thead>
            <tbody>
            <tr v-for="(course, index) in courses" :key='index'>
                <td>{{index + 1}}</td>
                <td>{{ course.title }}</td>
                <td>{{ course.semester }}</td>
                <td>{{ course.grade }}</td>
            </tr>
            </tbody>
        </table>
        <br>
        <br>
        <div>
            <button id="add-course-button" v-on:click="showPlus = !showPlus" class="blue-button">+</button>
            <span v-show="showPlus" id="add-course">
                <input class="input" type="text" placeholder="Course title" id="title" ref="title">
                <input class="input" type="number" min="1" max="8" placeholder="Semester" id="semester" ref="semester">
                <input class="input" type="number" min="0" max="100" placeholder="Grade" id="grade" ref="grade">
                <button class="green-button" id="save-course" v-on:click="saveCourse" >Save</button>
                <button class="grey-button" id="cancel-course" v-on:click="cancelCourse">Cancel</button>
            </span>
        </div>
    </div>
</template>

<script>
    import Course from '../models/Course'
    export default {
        name: 'CoursesTab',
        methods:{
            saveCourse: function(){
                this.courses.push(new Course(
                this.$refs.title.value,
                this.$refs.semester.value,
                this.$refs.grade.value
                )),
                this.cancelCourse()
                
            },
            cancelCourse: function(){
                this.$refs.title.value = "",
                this.$refs.semester.value = "",
                this.$refs.grade.value = "",
                this.showPlus = !this.showPlus
            }
        },
        props: {
            show: Boolean,
            showPlus: Boolean,
            courses: Array
        },
    }
</script>

<style>
    .input {
        border: 1px solid #cccccc;
        padding: 10px 20px;
        min-width: 135px;
        margin: 2px;
    }
    .blue-button {
        background-color: #2196F3;
        color: #ffffff;
        border: none;
        padding: 10px 20px;
    }
    .green-button {
        background-color: #69f378;
        color: #ffffff;
        border: none;
        padding: 10px 10px;
        margin-right: 2px;
    }
    .grey-button {
        background-color: #e1e8e6;
        color: #ffffff;
        border: none;
        padding: 10px 20px;
    }
</style>