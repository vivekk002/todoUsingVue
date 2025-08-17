<template>
    <form class="add-form" @submit.prevent="addTodo">
        <div class="f-header">
            <h1 class="f-h1">Add a New Task</h1>
            <p class="f-p">What do you want to get done?</p>
        </div>
        <div class="f-body">
            <h3 class="f-h3">Title</h3>
            <input 
            class="f-inputTitle" 
            type="text" placeholder="e.g., Buy groceries" 
            v-model="title"/>
            <h3 class="f-h3">Description (Optional)</h3>
            <textarea 
            class="f-textarea" 
            type="text" 
            placeholder="e.g. Milk, Bread, eggs.." 
            v-model="description"></textarea>
            
        </div>
        <div class="f-body">
            <label>Date</label>
            <input class="datePicker" v-model="date" type="date" />
        <Button type="submit"  /></div>
    </form>
</template>

<script setup>
import Button from './Button.vue';
import { ref } from 'vue'
import '@vuepic/vue-datepicker/dist/main.css'

const emit = defineEmits(["add-todo"])

const title = ref("")
const description = ref("")
const date = ref("")

const addTodo =()=>{
   
    
    if(!title._value || !description._value || !date._value){
        alert("Fill all the fields")
    }

    emit("add-todo",{
        title:title._value,
        description:description._value,
        date:date._value
    })

    title.value ="",
    description.value="",
    date.value=""
   
}

</script>