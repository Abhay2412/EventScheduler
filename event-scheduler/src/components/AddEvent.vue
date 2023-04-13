<template>
    <form @submit="onSubmit" class="add-form">
        <div class="form-control">
            <label>Event</label>
            <input type="text" v-model="text" name="text" placeholder="Add Event"/>
        </div>
        <div class="form-control">
            <label>Day & Time</label>
            <input type="text" name="day" v-model="day" placeholder="Add Day & Time"/>
        </div>
        <div class="form-control form-control-check">
            <label>Set Reminder</label>
            <input type="checkbox" v-model="reminder" name="reminder"/>
        </div>

        <input type="submit" value="Save Event" class="btn btn-block"/>
    </form>
</template>

<script>
export default {
    name: "AddEvent",
    data() {
        return {
            text: "",
            day: "",
            reminder: false
        }
    },
    methods: {
        onSubmit(e) {
            e.preventDefault()

            if(!this.text) {
                alert("Please add an event")
                return
            }
            const newEvent = {
                text: this.text,
                day: this.day,
                reminder: this.reminder
            }
            this.$emit("add-event", newEvent)
            this.text = ""
            this.day = ""
            this.reminder = false
        }
    }
}
</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
  color: #896B9A;
}
.form-control {
  margin: 20px 0;
}
.form-control label {
  display: block;
}
.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
  background: #FBFCE0;
}
.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.form-control-check label {
  flex: 1;
}
.form-control-check input {
  flex: 2;
  height: 20px;
}
</style>