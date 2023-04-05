<template>
    <div>
        <h1>My ToDo List</h1>
        <add-task @addTask="addTask"></add-task>
        <div class="todo-list">
            <ul class="todo-list-items">
                <li v-for="task in tasks" :key="task.id" class="todo-list-item">
                    <span v-if="!task.editing">{{ task.text }}</span>
                    <span v-else>
                        <input type="text" v-model="task.text">
                        <button @click="finishEditing(task)" class="todo-list-button">Update</button>
                        <button @click="cancelEditing(task)" class="todo-list-button">Cancel</button>
                    </span>
                    <button v-if="!task.editing" @click="startEditing(task)" class="todo-list-button">Edit Task</button>
                    <delete-task :task="task" @deleteTask="deleteTask"></delete-task>
                </li>
            </ul>
            <edit-task v-if="editingTask" :task="editingTask.task" @edit-task="finishEditing"
                @cancel-edit="cancelEditing"></edit-task>
        </div>
    </div>
</template>
<style>
.todo-list {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

.todo-list-items {
  list-style: none;
  padding: 0;
  margin: 0;
}

.todo-list-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 10px;
  padding: 10px;
  background-color: #f7f7f7;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 16px;
}

.todo-list-item span:first-child {
  flex: 1;
}

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

input[type="text"] {
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 5px 10px;
  margin-right: 10px;
}
</style>

<script>
import AddTask from './AddTask.vue'
import EditTask from './EditTask.vue'
import DeleteTask from './DeleteTask.vue'
import { Task } from './Task.js'

export default {
    name: 'ToDoList',
    components: {
        AddTask,
        EditTask,
        DeleteTask
    },
    data() {
        return {
            tasks: [
                new Task(1, 'Learn Vue'),
                new Task(2, 'Learn Vuex'),
                new Task(3, 'Learn Vue Router')
            ],
            nextTaskId: 4,
            editingTask: null
        }
    },
    methods: {
        addTask(newTaskText) {
            this.tasks.push({
                id: this.nextTaskId++,
                text: newTaskText
            })
        },
        startEditing(task) {
            // create a new Task object for editing purposes
            const editingTask = new Task(task.id, task.text);
            editingTask.editing = true;

            this.editingTask = {
                task: editingTask,
                editing: true
            };
        },
        finishEditing(updatedTask) {
            updatedTask.editing = false;
            const taskIndex = this.tasks.findIndex(task => task.id === updatedTask.id);
            this.tasks[taskIndex].text = updatedTask.text;
            this.editingTask = null;
        },
        cancelEditing() {
            this.editingTask.task.editing = false;
            this.editingTask = null;
        },
        deleteTask(taskId) {
            const taskIndex = this.tasks.findIndex(task => task.id === taskId)
            this.tasks.splice(taskIndex, 1)
        }
    }
}
</script>