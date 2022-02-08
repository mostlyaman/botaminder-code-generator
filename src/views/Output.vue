<template>
Hello World
{{Events}}
</template>


<script>
export default {
    name: 'Output',
    props: {
        events: Array
    },
    data() {
        return {
            Events: []
        }
    },
    mounted(){
        let count = 0;
        let data = this.$route.params.events;
        while(count < data.length){
            this.Events.push(JSON.parse(data[count]));
            count++;
        }
    },
}
</script>