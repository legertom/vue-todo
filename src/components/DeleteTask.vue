<template>
    <button @click="deleteTask" class="todo-list-button-delete">Delete</button>
</template>

<script>
export default {
    name: 'DeleteTask',
    props: ['task'],
    methods: {
        deleteTask() {
            this.$emit('deleteTask', this.task.id)
        }
    }
}
</script>