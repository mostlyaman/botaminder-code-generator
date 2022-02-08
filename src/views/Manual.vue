<template>
    <h1>Add Events Manually</h1>
    <Editor :events='events' />
</template>

<script>
import Editor from '@/components/Editor.vue'
export default {
    name: "Manual",
    data() {
        return{
            events: []
        }
    },
    components: {
        Editor,
    },
}
</script>

<style>
h1 {
    padding-bottom: 20px;
}
</style>