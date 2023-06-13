<template>
  <main>


    <!--heading-->
    <header>
    <img src="./components/icons/logo.svg" alt="pinia-logo">
    <h1>Pinia Tasks</h1>
  </header>
    <!---New task form-->
    <div class="new-task-form">
      <TaskForm/>
    </div>

 
   <!--Filter navs-->
   <nav class="filter">
   <button @click="filter='all'" >All</button>
   <button @click="filter='favs'" >Favorite</button>
   <button @click="TaskStore.$reset">Reset</button>
  </nav>


  <div class="loading" v-if="TaskStore.isloading">Loading Tasks...</div>
 
   
    <!---Task list-->
    <div class="task-list" v-if="filter==='all'">
      <p>You have {{ TaskStore.totalCount}} tasks left to do</p>
     <div v-for="task in TaskStore.tasks">
      <TaskDetails :task="task" />
      </div>
      </div>

      <div class="task-list" v-if="filter==='favs'">
        <p>You have {{ TaskStore.favCount }} favs left to do </p>
     <div v-for="task in TaskStore.favs">
      <TaskDetails :task="task" />
      </div>
      </div>

   


  </main>
</template>

<script>
import { storeToRefs } from 'pinia'
import TaskForm from './components/TaskForm.vue'
import TaskDetails from './components/icons/TaskDetails.vue'
import {useTaskStore} from './components/icons/TaskStore'
import {ref} from 'vue'
  export default {
    components:{ TaskDetails, TaskForm },
    setup (){
      const TaskStore =useTaskStore()
      const { tasks, loading,favs,totalCount,favCount} =storeToRefs(TaskStore)

      TaskStore.getTasks()
      const filter=ref('all')

      return {TaskStore,filter,tasks, loading,favs,totalCount,favCount}

    }
    
  }
</script>