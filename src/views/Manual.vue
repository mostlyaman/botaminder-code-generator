<template>
    <h1>Add Events Manually</h1>
    <Editor :events='events' />
    <Footer></Footer>
</template>

<script>
import Editor from '@/components/Editor.vue'
import Footer from '@/components/Footer.vue'
export default {
    name: "Manual",
    data() {
        return{
            events: []
        }
    },
    components: {
        Editor,
        Footer
    },
}
</script>

<style>
h1 {
    padding-bottom: 20px;
}
</style>