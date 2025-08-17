<template>
  
<div :class="t.completed ? 'checkedDiv' : 'checkbox-div'"
class="checkbox-div"
v-for="t in props.todos"
:key="id">
    <div >
        <label class="checkbox-label">
      <input class="checkbox" 
      type="checkbox" 
      :checked="t.completed"
      @change="$emit('toggle-completed',t.id,$event.target.checked)"
      />
      {{ t.title }}
    </label>
    <p class="checkbox-p">{{ t.description }}</p>
    <small class="checkbox-date">Finish till: {{ fmtDate(t.date) }}</small>
   
    </div>
    <div>
        <button @click="$emit('openUpdate',t.id)" class="iconbutton">
        <font-awesome-icon :icon="['fas','pen']" class="penicon" />
    </button>
        <button @click="$emit('delete',t.id)" class="iconbutton">
            <font-awesome-icon :icon="['fas','trash']" class="trashicon" />
        </button>
    </div>
  </div>

</template>

<script setup>
const props = defineProps({
  todos: {
    type: Array,
    required: true,
    default: () => []
  }
})



import { ref, watchEffect } from 'vue'

const checked = ref(false)

watchEffect(()=>{
    if(props.todos && props.todos.length != checked.value.length) {
        checked.value = props.todos.map((todo) => false) 
    }
})

function fmtDate(d) {
  // d can be "2025-08-28" or a Date
  const dt = (d instanceof Date) ? d : new Date(d)
  if (Number.isNaN(dt.getTime())) return String(d) // fallback
  return dt.toLocaleDateString('en-IN') // 28/08/2025
}

defineEmits(["delete","openUpdate","toggle-completed"])
</script>
