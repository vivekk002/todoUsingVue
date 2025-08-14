<template>
  
<div class="checkbox-div" :class="{ checkedDiv: checked }">
    <div >
        <label class="checkbox-label">
      <input class="checkbox" type="checkbox" v-model="checked" />
      Subscribe to newsletter
    </label>
    <p class="checkbox-p">Checked: {{ checked }}</p>
    </div>
    <div>
        <font-awesome-icon :icon="['fas','pen']" class="penicon" />
        <font-awesome-icon :icon="['fas','trash']" class="trashicon" />
    </div>
  </div>
  
    
  
</template>

<script setup>

import { ref } from 'vue'
const checked = ref(false)

</script>
