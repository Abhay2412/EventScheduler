<template>
    <header>
        <h1 :style="{color: textColor}">{{ title }}</h1>
        <Button v-if="homePage" @btn-click="$emit('toggle-add-event')" :text="showAddEvent ? 'Close' : 'Add Event'" :color="showAddEvent ? '#FF8080' : '#9BC995'"/>
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
        Button,
    },
    computed: {
        homePage() {
            if(this.$route.path === "/") {
                return true
            } 
            else {
                return false
            }
        }
    },
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