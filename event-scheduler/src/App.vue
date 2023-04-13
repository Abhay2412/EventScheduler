<template>
  <div class="container">
    <Header @toggle-add-event="toggleAddEvent" title="Event Scheduler" :showAddEvent="showAddEvent" textColor="#5171A5"/>
    <div v-if="showAddEvent">
      <AddEvent @add-event="addEvent"/>
    </div>
    <Events @toggle-reminder="toggleReminder" @delete-event="deleteEvent" :events="events"/>
  </div>
</template>

<script>
import Header from "./components/Header"
import Events from "./components/Events"
import AddEvent from "./components/AddEvent"

export default {
  name: 'App',
  components: {
    Header,
    Events,
    AddEvent,

  },
  data() {
    return {
      events: [],
      showAddEvent: false
    }
  },
  methods: {
    toggleAddEvent() {
      this.showAddEvent = !this.showAddEvent
    },
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
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #9BC995;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>