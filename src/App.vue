<script setup>
import {ref,onMounted,computed} from 'vue'

const task = ref("")
const search = ref("")
const total =ref(0)
const show = ref(false)
const todos = ref([])

const addTask=(e)=>{
                    e.preventDefault();
                    const todo = {
                        task:task.value,
                        status:false
                    }
                    todos.value.push(todo)
                    task.value=""
}

const removeTask=(id)=>{
     todos.value.splice(id,1)
}

const getDataFromTheServer=()=>{
                    const newObj=[
                        {
                            task:"Walk in the park",
                            status:false
                        },
                        {
                            task:"Eat breakfast",
                            status:true
                        }
                    ]
              todos.value=newObj
}
const markAsDone=(todo)=>{
                    todo.status=!todo.status
                }
const showForm=()=>{
                    show.value=!show.value
 }

 onMounted(()=>{
  getDataFromTheServer()
 })

 const filterTodos = computed(()=>{
  return todos.value.filter(todo=>{
       return todo.task.toLowerCase().includes(search.value.toLowerCase())
  })
 })
 const totalTasks = computed(()=>{
  return total.value=todos.value.length
 })

</script>

<template>
  <div>
    <button @click="showForm">show</button>
        <form v-if="show" @submit="addTask">
            <input type="text" placeholder="Add task..." v-model="task" required>
            <button type="submit">Submit</button>
        </form>
        <div v-else>
            <p>NO form shown</p>
        </div>
        <input type="text " placeholder="Search here.." v-model="search">
        <p>Total Task: {{totalTasks}}</p>
        <table>
            <thead>
                <tr>
                    <th>Task</th>
                    <th>Status</th>
                    <th>Action</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(todo,index) in filterTodos" :class="todo.status ?'done':''">
                    <td>{{todo.task}}</td>
                    <td>{{todo.status}}</td>
                    <td>
                        <button @click="removeTask(index)">Remove</button>
                        <button @click="markAsDone(todo)">Done</button>
                    </td>
                </tr>
            </tbody>
        </table>
  </div>
</template>

<style>
 table,tr,td,th{
            border:1px solid;
        }
        .done{
            background-color: aquamarine;
        }
        .hide{
            display:none;
        }
        form{
            border:1px solid;
            padding:10px;
            margin:10px
        }
</style>
