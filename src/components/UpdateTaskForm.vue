<template>
  <div v-if="open" class="dialog-backdrop" @click.self="onCancel">
    <div class="dialog">
      <h3>Edit Todo</h3>
      <form @submit.prevent="onSave">
        <label>Title</label>
        <input v-model="form.title" placeholder="Title" />

        <label>Description</label>
        <textarea v-model="form.description" placeholder="Description"></textarea>

        <label>Date</label>
        <input v-model="form.date" type="date" />

        <div class="actions">
          <button type="button" @click="onCancel">Cancel</button>
          <button type="submit">Save</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script setup>
import { reactive, watch } from 'vue';


const props = defineProps({
    open:{
        type:Boolean,
        required:true
    },
    todo:{
        type:Object,
        default:()=>({
            id:null,
            title:"",
            description:"",
            date:""
        })
    }
})
const emit = defineEmits(["close" , "update"]);

const form = reactive({
    id:props.todo.id,
    title:"",
    description:"",
    date:""
})

watch(()=>props.todo,(t)=>{
    form.title = t.title;
    form.description = t.description;
    form.date = t.date;
},{immediate:true , deep:false})


const onCancel = ()=>{
    emit("close");
}

const onSave = ()=>{
    if(!form.title || !form.description || !form.date) return;
    emit('update',{
        id:props.todo.id,
        title:form.title,
        description:form.description,
        date:form.date
    })
}
</script>