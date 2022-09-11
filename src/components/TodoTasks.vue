<template>
  <div v-for="task in tasks" :key="task.id">
    <TodoTask
      @toggle-reminder="$emit('toggle-reminder', task.id)"
      @delete-task="$emit('delete-task', task.id)"
      :task="task"
    />
  </div>
</template>
<script>
import TodoTask from "./TodoTask.vue";

export default {
  name: "TodoTasks",
  props: {
    tasks: Array,
  },
  components: {
    TodoTask,
  },
  emits: ["delete-task", "toggle-reminder"],
};
</script>
