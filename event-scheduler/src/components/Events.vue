<template>
    <div>
        <div :key="event.id" v-for="event in events">
            <h3 :style="{ color: eventHeadingColor}">{{ event.text }}</h3>
        </div>
    </div>
</template>

<script>
 export default {
    name: "Events",
    props: {
        events: Array,
        eventHeadingColor: String,
    },
 }
</script>