<template>
    <button @click="addTask()" :style="{background:color}" class="btn">{{text}}</button>
</template>

<script lang="ts">
    export default{
        name:"Button",
        props:{
            text:{
                type:String,
                default:"Add Task"
            },
            color:String
        },
        methods:{
            addTask(){
                console.log("Hi");
            }
        },
    }
</script>