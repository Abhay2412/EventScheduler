<template>
    <header>
        <h1 :style="{color: textColor}">{{ title }}</h1>
        <Button text="Add Event" color="#9BC995"/>
    </header>
</template>

<script>
import Button from "./Button"
export default {
    name: "Header",
    props: {
        title: String,
        textColor: String
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