<template>
<div class="tools">
    <w-button @click = "this.$emit('add-event-field')" class = "ma1">Add Event</w-button>
    <w-button @click = "this.$emit('reset-all-events')" class = "ma1 reset" type = "reset">Reset</w-button>
    <w-button class = "ma1" bg-color = "success" type = "submit">Submit</w-button>
</div>
</template>

<script>
export default {
    name: 'Tools',
}
</script>

<style scoped>
.tools {
    padding: 10px;
}
.reset {
    background-color: red;
}
</style>
