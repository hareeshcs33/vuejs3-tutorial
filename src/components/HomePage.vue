<template>
  <div class="home">Home</div>
  <HeaderPage
    @toggle-add-task="ToggleAddTask"
    title="Header"
    :showAddTask="showAddTask"
  />
  <AddTask v-show="showAddTask" @add-task="AddTask" />
  <TodoTasks
    @toggle-reminder="toggleReminder"
    @delete-task="deleteTask"
    :tasks="tasks"
  />
</template>

<script>
import HeaderPage from "./HeaderPage.vue";
import TodoTasks from "./TodoTasks.vue";
import AddTask from "./AddTask.vue";

export default {
  name: "HomePage",
  props: {},
  data() {
    return {
      tasks: [],
      showAddTask: false,
    };
  },
  components: {
    HeaderPage,
    TodoTasks,
    AddTask,
  },
  methods: {
    ToggleAddTask() {
      this.showAddTask = !this.showAddTask;
    },
    async deleteTask(id) {
      if (confirm("Are you sure?")) {
        const res = await fetch(`api/tasks/${id}`, {
          method: "DELETE",
        });
        res.status === 200
          ? (this.tasks = this.tasks.filter((task) => task.id !== id))
          : alert("Error deleting task");
      }
    },
    async toggleReminder(id) {
      const taskToToggle = await this.fetchTask(id);
      const updTask = { ...taskToToggle, reminder: !taskToToggle.reminder };
      const res = await fetch(`api/tasks/${id}`, {
        method: "PUT",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(updTask),
      });
      const data = await res.json();
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: data.reminder } : task
      );
    },
    async AddTask(newTask) {
      const res = await fetch("api/tasks", {
        method: "POST",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(newTask),
      });

      const data = await res.json();

      this.tasks = [...this.tasks, data];
    },
    async fetchTasks() {
      const res = await fetch("api/tasks");
      const data = await res.json();
      return data;
    },
    async fetchTask(id) {
      const res = await fetch(`api/tasks/${id}`);
      const data = await res.json();
      return data;
    },
  },
  async created() {
    this.tasks = await this.fetchTasks();
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped src="../styles/home-page.css"></style>
