<template>
    <div>
        <div :key="event.id" v-for="event in events">
            <Event :event="event"/>
        </div>
    </div>
</template>

<script>
import Event from "./Event"

 export default {
    name: "Events",
    props: {
        events: Array,
    },
    components: {
        Event
    },
 }
</script>