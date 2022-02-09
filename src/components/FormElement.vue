<template>
    <w-input class = "ma1" :default = "event.name" v-model = "event.name" :validators = "[validators.required, validators.length]">
        Event Name
    </w-input>
    <w-flex>
        <w-input class = "xs6" :default = "startTime" type = "time" v-model = "startTime">Event Time</w-input>
        <w-input class="xs6" :default = "endTime" type = "time" v-model = "endTime">Event End Time</w-input>
    </w-flex>
</template>

<script>
export default {
    name: 'FormElement',
    props: {
        event: Object,
    },
    data(){
        return{
            startTime: String,
            endTime: String,
            validators: {
                required: value => !!value || 'This field is required',
                length: value => value.length < 17 || 'LCD display can display a max length of 16 characters'
            }
        }
    },
    created(){
        let a = "";
        if(this.event.startHour < 10){
            a += "0";
        }
        a += this.event.startHour.toString();
        a+=":";
        if(this.event.startMin < 10){
            a += "0";
        }
        a+= this.event.startMin.toString();
        this.startTime = a;

        a = "";
        if(this.event.endHour < 10){
            a += "0";
        }
        a += this.event.endHour.toString();
        a+=":";
        if(this.event.endMin < 10){
            a += "0";
        }
        a+= this.event.endMin.toString();
        this.endTime = a;
    },
    watch: {
        startTime(newTime){
            this.event.startHour = parseInt(newTime.substring(0,2));
            this.event.startMin = parseInt(newTime.substring(3,5));
        },
        endTime(newTime){
            this.event.endHour = parseInt(newTime.substring(0,2));
            this.event.endMin = parseInt(newTime.substring(3,5));
        },
        event(newEvent){
            let a = "";
            if(newEvent.startHour < 10){
                a += "0";
            }
            a += newEvent.startHour.toString();
            a+=":";
            if(newEvent.startMin < 10){
                a += "0";
            }
            a+= newEvent.startMin.toString();
            this.startTime = a;

            a="";
            if(newEvent.endHour < 10){
                a += "0";
            }
            a += newEvent.endHour.toString();
            a+=":";
            if(newEvent.endMin < 10){
                a += "0";
            }
            a+= newEvent.endMin.toString();
            this.endTime = a;

        }
    },
}
</script>

<style scoped>
* {
    padding:10px;
}
</style>