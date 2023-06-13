
<template>
  <form @submit.prevent="handlesubmit">
<input type="text"  v-model="newTask" placeholder="add a new task to do...">

<button>Add</button>
  </form>
 
</template>

<script>
import { useTaskStore } from './icons/TaskStore';
import {ref} from 'vue'

export default {
  setup()
  {
    const taskStore=useTaskStore()
    const newTask=ref('')


    const handlesubmit=()=>{
      if(newTask.value.length>0)
      {
        taskStore.addTask({
          title:newTask.value,
          isFav:false,
          id: Math.floor(Math.random()*10000)
        })
        newTask.value=''

        }
      }
      return {handlesubmit,newTask}
    },

  }

</script>

<style >

</style>

