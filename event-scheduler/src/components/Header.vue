<template>
    <header>
        <h1 :style="{color: textColor}">{{ title }}</h1>
        <Button @btn-click="$emit('toggle-add-event')" :text="showAddEvent ? 'Close' : 'Add Event'" :color="showAddEvent ? '#FF8080' : '#9BC995'"/>
    </header>
</template>

<script>
import Button from "./Button"
export default {
    name: "Header",
    props: {
        title: String,
        textColor: String,
        showAddEvent: Boolean,
    },
    components: {
        Button
    }
}
</script>

<style scoped>
 header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
 }
</style>