<template>
  <div class="container">
    <div>
      <h1><strong>Todo List</strong></h1>
    </div>
    <div class="list-task">
      <div v-if="tasks.length === 0" class="empty-task">Belum ada Task</div>
      <div v-else>
        <div v-for="item of tasks" class="item-task d-flex align-items-start border-bottom pt-3 pb-4">
          <input type="checkbox" name="status" id="task" class="me-2 mt-2" :checked="item.isDone" @change="toggleTaskStatus(item)" />
          <div class="d-flex flex-column">
            <div class="title-task mb-1" :class="{ 'task-done': item.isDone }">
              {{ item.title }}
            </div>
            <div class="description-task small text-muted">
              {{ item.description }}
            </div>
            <a href="#" @click="deleteTask(index)">Delete</a>
          </div>
        </div>
      </div>
    </div>
    <div class="action py-2">
      <!-- <a href="#" class="add-button">Add Task</a> -->
      <a href="#" class="add-button" v-if="!isCreating" @click="isCreating = !isCreating">Add Task</a>
      <div class="add-card" v-else>
        <div class="card mb-2">
          <div class="card-body d-flex flex-column p-0">
            <input v-model="titleValue" class="form-control border-0 mb-2" placeholder="Title" type="text" />
            <textarea v-model="descriptionValue" class="form-control border-0 small" placeholder="Description" rows="3"></textarea>
          </div>
        </div>
        <div class="button-wrapper d-flex">
          <button class="btn btn-primary me-2" @click="addTask">Save</button>
          <button class="btn btn-outline-secondary" @click="isCreating = !isCreating">Cancel</button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import "bootstrap/dist/css/bootstrap.css";
import "bootstrap-vue/dist/bootstrap-vue.css";
export default {
  data() {
    return {
      // Daftar task
      tasks: [],
      isCreating: false,
      titleValue: "",
      descriptionValue: "",
    };
  },
  methods: {
    addTask() {
      this.tasks.push({
        title: this.titleValue,
        description: this.descriptionValue,
        isDone: false,
      });
      this.titleValue = "";
      this.descriptionValue = "";
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    toggleTaskStatus(task) {
      task.isDone = !task.isDone;
    },
  },
};
</script>
<style>
.task-done {
  text-decoration: line-through;
}
</style>
