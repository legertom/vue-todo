<template>
    <form @submit.prevent="editTask">
      <label for="editTask">Edit Task</label>
      <input type="text" v-model="editedTask" />
      <button class="todo-list-button" type="submit">Update Task</button>
      <button class="todo-list-button-delete" type="button" @click="cancelEdit">Cancel</button>
    </form>
  </template>
  
  <style>
.todo-list-button {
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 5px;
  padding: 5px 10px;
  cursor: pointer;
  margin-left: 10px;
}

.todo-list-button-delete {
  background-color: white;
  color: gray;
  border: none;
  border-radius: 5px;
  padding: 5px 10px;
  cursor: pointer;
  margin-left: 10px;
}

.todo-list-button-delete:hover{
    background-color: #f44336;
    color: white;
}

.todo-list-button:hover {
  background-color: #3e8e41;
}
</style>
  <script>
  export default {
    name: "EditTask",
    props: ["task"],
    data() {
      return {
        editedTask: this.task.text,
      };
    },
    methods: {
      editTask() {
        this.$emit("edit-task", {
          id: this.task.id,
          text: this.editedTask,
        });
      },
      cancelEdit() {
        this.$emit("cancel-edit");
      },
    },
  };
  </script>
  