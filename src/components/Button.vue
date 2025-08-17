<template>

    <button class="button" @click="$emit('click')" >Submit</button>
</template>

<script setup>
defineEmits(["click"])
</script>