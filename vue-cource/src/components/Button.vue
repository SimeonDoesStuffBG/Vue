<template>
    <button @click="addTask()" :style="{background:color}" class="btn">{{text}}</button>
</template>

<script>
    export default{
        name:"Button",
        props:{
            text:{
                type:String,
                default:'I am a button'
            },
            color:{
                type:String,
                default:'green'
            }
        },
        methods:{
            addTask(){
                this.$emit('btn-click');
            }
        },
    }
</script>