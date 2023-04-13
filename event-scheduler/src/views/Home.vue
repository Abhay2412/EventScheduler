<template>
    <AddEvent v-if="showAddEvent" @add-event="addEvent"/>
    <Events @toggle-reminder="toggleReminder" @delete-event="deleteEvent" :events="events"/>
</template>

<script>
import Events from "../components/Events"
import AddEvent from "../components/AddEvent"
export default {
    name: "Home",
    props: {
        showAddEvent: Boolean,
    },
    components: {
        Events,
        AddEvent,
    },
    data() {
        return {
            events: [],
        }
    },
    methods: {
    async addEvent(event) {
      const response = await fetch("api/events", {
        method: "POST",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(event),
      })
      
      const data = await response.json()

      this.events = [...this.events, data]
    },
    async deleteEvent(id) {
      if(confirm("Remove this event?")) {
        const response = await fetch(`api/events/${id}`, {
          method: "DELETE"
        })

        response.status === 200 ? (this.events = this.events.filter((event) => event.id !== id)) : alert("Error deleting in event")
      }
    },
    async toggleReminder(id) {
      const eventToToggle = await this.fetchEvent(id)
      const updateEvent = {...eventToToggle, reminder: !eventToToggle.reminder}

      const response = await fetch(`api/events/${id}`, {
        method: "PUT",
        headers: {
          "Content-type": "application/json"
        },
        body: JSON.stringify(updateEvent)
      })
      
      const data = await response.json()

      this.events = this.events.map((event) => event.id === id ? {...event, reminder: data.reminder} : event)
    },
    async fetchEvents() {
      const response = await fetch("api/events")

      const data = await response.json()

      return data
    },
    async fetchEvent(id) {
      const response = await fetch(`api/events/${id}`)

      const data = await response.json()

      return data
    },
  },
  async created() {
    this.events = await this.fetchEvents()
  },
}
</script>