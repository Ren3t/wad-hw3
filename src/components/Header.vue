<template>
    <header>
        <strong>{{message}}</strong>
    </header>
</template>

<script>
    export default {
        name: "Header",
        data: function(){
            return {
                message:"Welcome to your dashboard!"
            }
        }
    }
</script>

<style>
    header {
        padding: 20px;
        background-color: #2196F3;
        color: #ffffff;
        text-align: center;
        margin-bottom: 10px;
        height: 60px;
    }
</style>