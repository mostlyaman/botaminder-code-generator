<template>
    <div class="container2">
        <w-form @reset = "removeAllEvents" @success = "submitEvents" v-model = "formValid">
        <div :key="event.id" v-for="event in events" class="form">
            <h3>Event {{ event.id+1 }}</h3>
            <FormElement :event = "event" />
        </div>
        <Tools @add-event-field = "addEventField"  />
        </w-form>
    </div>
</template>

<script>
import Tools from './Tools.vue'
import FormElement from './FormElement.vue'
export default {
    name: 'Editor',
    props: {
        events: Array,
    },
    data(){
        return{
            formValid: null,
        }
    },
    components: {
        Tools,
        FormElement
    },
    created(){
        if(this.events.length === 0){
            this.events.push({
                id: 0,
                name: "",
                hour: 0,
                min: 0
            })
        }
    },
    methods: {
        addEventField(){
            let newField = this.events.at(-1).id + 1;
            this.events.push({
                id: newField,
                name: "",
                hour: 0,
                min: 0
            })
        },
        removeAllEvents(){
            this.events.length=1;
            this.events[0] = {
                id: 0,
                name: "",
                hour: 0,
                min: 0
            }
            this.formValid = null;
        },
        submitEvents(){
            let e = 0;
            let data = [];
            while(e < this.events.length){
                if(this.events[e].hour === NaN || this.events[e].min === NaN){
                    alert('Not defined hour or min');
                    return;
                }
                data.push(JSON.stringify(this.events[e]));
                e++;
            }
            this.$router.push({name: 'Output', params: {events: data}});
        }
    },
}
</script>

<style scoped>
.container2 {
    min-width: 500px;
    background-color: rgb(213, 236, 236);
    border-radius: 5px;
    align-self: center;
}
h3 {
    padding:15px;
}
</style>