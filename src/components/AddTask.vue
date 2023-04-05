<template>
    <form @submit.prevent="addTask">
        <label for="newTask">Add a new task</label>
        <input type="text" v-model="newTask" />
        <button type="submit">Add Task</button>
    </form>
</template>

<script>
export default {
    name: 'AddTask',
    data() {
        return {
            newTask: ''
        }
    },
    methods: {
        addTask() {
            this.$emit('addTask', this.newTask)
            this.newTask = ''
        }
    }
}
</script>