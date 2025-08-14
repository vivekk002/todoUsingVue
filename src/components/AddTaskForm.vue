<template>
    <form class="add-form">
        <div class="f-header">
            <h1 class="f-h1">Add a New Task</h1>
            <p class="f-p">What do you want to get done?</p>
        </div>
        <div class="f-body">
            <h3 class="f-h3">Title</h3>
            <input class="f-inputTitle" type="text" placeholder="e.g., Buy groceries" />
            <h3 class="f-h3">Description (Optional)</h3>
            <textarea class="f-textarea" type="text" placeholder="e.g. Milk, Bread, eggs.." ></textarea>
            
        </div>
        <div class="f-body">
            <VueDatePicker v-model="date" :enable-time-picker="false" placeholder="Select date" />
        <Button /></div>
    </form>
</template>

<script setup>
import Button from './Button.vue';
import { ref } from 'vue'
import VueDatePicker from '@vuepic/vue-datepicker'
import '@vuepic/vue-datepicker/dist/main.css'
const date = ref(null) // will hold a Date or string depending on props

</script>