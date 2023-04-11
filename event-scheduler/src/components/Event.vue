<template>
    <div :class="[event.reminder ? 'reminder' : '', 'event']">
        <h3 :style="{ }">{{ event.text }}
        <i @click="onDelete(event.id)" class="fas fa-times"></i>
        </h3>
        <p>{{ event.day }}</p>
    </div>
</template>

<script>
export default {
    name: "Event", 
    props: {
        event: Object,
    },
    methods: {
        onDelete(id) {
            this.$emit("delete-event", id)
        }
    }
}
</script>

<style>
.fas {
  color: #FF8080;
}
.event {
  background: #ECE3F0;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}
.event.reminder {
  border-left: 5px solid #44A47C;
}
.event h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
  color: #CED32F;
}
</style>
