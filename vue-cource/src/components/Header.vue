<template>
    <header>
        <h1>{{title}}</h1>
        <Button color="green"/>
    </header>
</template>

<script lang="ts">
    import Button from './Button.vue';

    export default{
        name:'Header',
        props:{
            title:String,
        },
        components:{
            Button,
        }
    }
</script>

<style scoped>
    header{
        display:flex;
        justify-content: center;
        align-items: center;
        margin-bottom: 20px;
    }
</style>