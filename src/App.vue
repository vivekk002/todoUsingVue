
<template> 
<div>
    <Header />
    <AddTaskForm />
    <h1 class="a-h1">Your Tasks</h1>
    <TaskComponant/>
</div>
</template>

<script setup>

import AddTaskForm from './components/AddTaskForm.vue';
import Header from './components/Header.vue';
import TaskComponant from './components/TaskComponant.vue';
</script>