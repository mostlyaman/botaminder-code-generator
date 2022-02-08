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
        let data = this.$route.params.events;
        if(data != undefined){
            let count = 0;
            while(count < data.length){
            this.Events.push(JSON.parse(data[count]));
            count++;
            }
        }
    },
}
</script>