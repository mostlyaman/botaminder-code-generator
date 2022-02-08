<template>
    <w-input class = "ma1" :default = "event.name" v-model = "event.name" :validators = "[validators.required, validators.length]">
        Event Name
    </w-input>
    <w-input class = "ma1" :default = "time" type = "time" v-model = "time">Event Time</w-input>
</template>

<script>
export default {
    name: 'FormElement',
    props: {
        event: Object,
    },
    data(){
        return{
            time: String,
            validators: {
                required: value => !!value || 'This field is required',
                length: value => value.length < 17 || 'LCD display can display a max length of 16 characters'
            }
        }
    },
    created(){
        let a = "";
        if(this.event.hour < 10){
            a += "0";
        }
        a += this.event.hour.toString();
        a+=":";
        if(this.event.min < 10){
            a += "0";
        }
        a+= this.event.min.toString();
        this.time = a;
    },
    watch: {
        time(newTime){
            this.event.hour = parseInt(newTime.substring(0,2))
            this.event.min = parseInt(newTime.substring(3,5))
        },
        event(newEvent){
            let a = "";
            if(newEvent.hour < 10){
                a += "0";
            }
            a += newEvent.hour.toString();
            a+=":";
            if(newEvent.min < 10){
                a += "0";
            }
            a+= newEvent.min.toString();
            this.time = a;
        }
    },
}
</script>

<style scoped>
* {
    padding:10px;
}
</style>