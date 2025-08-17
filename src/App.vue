
<template> 
<div>
    <Header />
    <AddTaskForm @add-todo="addTodo"/>
    <h1 class="a-h1">Your Tasks</h1>
    <TaskComponant 
    :todos="todos" 
    @delete="handleDelete" 
    @openUpdate="handleUpdateDialog"
    @toggle-completed="toggleCompleted"/>
    
    <UpdateTaskForm 
    :open="editOpen"
    :todo="editTodo"
    @close="editOpen=false"
    @update = "updateTodo"
    />
</div>
</template>

<script setup>
import { onMounted } from 'vue';
import AddTaskForm from './components/AddTaskForm.vue';
import Header from './components/Header.vue';
import TaskComponant from './components/TaskComponant.vue';
import { ref } from 'vue';
import { watch } from 'vue';
import UpdateTaskForm from './components/UpdateTaskForm.vue';

const todos = ref([]);

onMounted(()=>{
    try{
        const savedTodos = localStorage.getItem("todos");
        if(savedTodos){
            const parsed = JSON.parse(savedTodos);
            if(Array.isArray(parsed)){
                todos.value =parsed,map(t=>({completed:false,...t}));
            }
        }
    }catch(error){
        console.error("Error loading  todos from localstorage:",error);
    }
});

watch(todos,(val)=>{
    localStorage.setItem("todos", JSON.stringify(val))
},{deep:true})

const todoId = () => {
  return Math.floor(Math.random() * 1000000);
}


const addTodo = (todo)=>{
    console.log("new todo", todo);
    todo.id = todoId();
    todo.completed = false;
    todos.value.push(todo);
    
}

const handleDelete = (id)=>{
    todos.value = todos.value.filter((todo)=> todo.id !== id);
}


const editOpen = ref(false);
const editTodo = ref({
    id:null,
    title:"",
    description:"",
    date:""
})

const handleUpdateDialog = (id)=>{
    const updateTodo = todos.value.find((todo)=>todo.id===id);
    if(!updateTodo) return;
    editTodo.value = {...updateTodo};
    editOpen.value = true;
}

const toggleCompleted = (id,value)=>{
    const todo = todos.value.find((todo)=>todo.id===id);
    if(!todo) return;
    todo.completed = value;
}

const updateTodo = (updatedTodo)=>{
    const idx = todos.value.findIndex((todo)=>todo.id === updatedTodo.id);
    if(idx!== -1){
        todos.value[idx] = updatedTodo;
    }
    editOpen.value=false;
}
</script>