<template>
    <main id="app">
        <app-header></app-header>
        <section id="container">
            <section id="main">
                <div class="content">
                    <Profile :user="user" :show="profileActive"/>
                    <Courses :courses="courses" :show="coursesActive"/>
                </div>
                <div class="controls">
                    <button id="profile-button" @click="togglePill" :class="{pill: true, active: profileActive}">Profile</button>
                    <button id="courses-button" @click="togglePill" :class="{pill: true, active: coursesActive}">Courses</button>
                </div>
            </section>
        </section>
        <app-footer></app-footer>
    </main>
</template>

<script>
    import Header from './components/Header.vue'
    import Footer from './components/Footer.vue'
    import Profile from './components/ProfileTab.vue'
    import Courses from './components/CoursesTab.vue'
    import User from "./models/User"
    import Course from './models/Course'
    

    export default {
        name: 'app',
        components: {
            'app-header': Header,
            'app-footer': Footer,
            Profile,
            Courses,
        },
        data: function() {
            return{
                user: new User("John","Doe","11/10/1990","Software Engineering","2.75"),
                courses :[
                    new Course("Agile software development", "1", "82"),
                    new Course("System modeling", "1", "85"),
                    new Course("Object-oriented programming", "2", "99"),
                    new Course("Estonian language Level A2", "2", "65") ],
                coursesActive : false,
                profileActive : true
            };
        
        },
        methods: {
            togglePill: function(){
                this.coursesActive = !this.coursesActive;
                this.profileActive = !this.profileActive;
                this.user.gpa = this.changeGPA();
            },
            changeGPA: function(){
                var points = 0;
                for(var i = 0;i<this.courses.length;i++){
                    if(this.courses[i].grade >90){
                        points += 4;
                    }
                    else if(this.courses[i].grade >80){
                        points += 3;
                    }
                    else if(this.courses[i].grade >70){
                        points += 2;
                    }
                    else if(this.courses[i].grade >60){
                        points += 1;
                    }
                    else if(this.courses[i].grade >50){
                        points += 0.5;
                    }
                    else{
                        points += 0;
                    }
                }
                var gpa = points/this.courses.length;
                return gpa
                }
            }
        }
</script>

<style>
    * {
        box-sizing: border-box;
        font-family: 'Livvic', sans-serif;
    }

    html, body {
        padding: 0;
        margin: 0;
        width: 100%;
        height: 100%;
        background-color: #eaeaea;
    }

    main {
        position: relative;
        min-height: 100%;
        padding-bottom: 110px;
    }

    .clear-fix {
        clear: both;
    }

    #container {
        width: 80%;
        max-width: 900px;
        min-width: 320px;
        padding: 15px;
        background-color: #ffffff;
        margin: 0 auto;
    }
    .content {
        padding: 10px;
        border: 1px solid #cbcbcb;
    }

    table {
        width: 100%;
        border-collapse: collapse;

    }

    table th {
        padding: 8px 12px;
        text-align: left;
        border: 1px solid #cbcbcb;
        background-color: #03A9F4;
        color: #ffffff;
    }

    table td {
        padding: 8px 12px;
        border: 1px solid #cbcbcb;
    }

    .content .tab {
        display: none;
    }

    .content .tab.active {
        display: block;
    }

    .controls .pill {
        border: 1px solid #cbcbcb;
        background-color: #eaeaea;
        padding: 10px;
        border-bottom-left-radius: 4px;
        border-bottom-right-radius: 4px;
        border-top: none;
        margin-top: -1px;
        outline: none !important;
    }

    .controls .pill.active {
        background-color: #ffffff;
        border-top: 1px solid #ffffff;
    }

    .controls .pill:hover {
        cursor: pointer;
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
    }

    .grey-button {
        background-color: #e1e8e6;
        color: #ffffff;
        border: none;
        padding: 10px 20px;
    }

    .input {
        border: 1px solid #cccccc;
        padding: 10px 20px;
        min-width: 135px;
    }
</style>
