<template>
    <div>
        <div :key="event.id" v-for="event in events">
            <Event @toggle-reminder="$emit('toggle-reminder', event.id)" @delete-event="$emit('delete-event', event.id)" :event="event"/>
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
    emits: ["delete-event", "toggle-reminder"]
 }
</script>