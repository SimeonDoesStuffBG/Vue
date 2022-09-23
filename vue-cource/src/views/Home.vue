<template>
    <div><AddTask v-if="showAddTask" @add-task="addTask"/></div>
    <Tasks @toggle-task="toggleTask" @delete-task="deleteTask" :tasks="tasks"/>
</template>

<script>
    import Tasks from '../components/Tasks';
    import AddTask from '../components/AddTask';

    export default{
        name:"Home",
        components:{
            Tasks,
            AddTask,
        },
        data(){
            return {
                tasks:[],
            }
        },
        methods:{
            //add and remove task
             async addTask(task){
                const res = await fetch('api/tasks', {
                    method:'POST',
                    headers:{
                        'Content-type':'application/json'
                    },
                    body:JSON.stringify(task)
                });
                const data=await res.json();
                this.tasks=[...this.tasks, data];
              },
              
              async deleteTask(id){
                const res= await fetch(`api/tasks/${id}`,{
                  method:'DELETE',
                });

                if(res.status===200){
                  this.tasks=this.tasks.filter(task=>task.id!==id);
                }else{
                  alert('Error while deleting');
                }
              },
              //alter task
              async toggleTask(id){
                const taskToToggle = await this.fetchTask(id);

                const updTask = {...taskToToggle, reminder:!taskToToggle.reminder};

                const res = await fetch(`api/tasks/${id}`,{
                  method:"PUT",
                  headers:{
                    'Content-type':'application/json'
                  },
                  body:JSON.stringify(updTask)
                });

                const data = await res.json();

                this.tasks=this.tasks.map(task=>(task.id===id)?{...task,reminder:data.reminder}:task);
              },
              //task getter
              async fetchTasks(){
                const res = await fetch("api/tasks");

                const data = await res.json();
                return data;
              },

              async fetchTask(id){
                const res = await fetch(`api/tasks/${id}`);

                const data = await res.json();

                return data;
              },
              async created(){
                this.tasks= await this.fetchTasks();
              }
            }
            }
</script>