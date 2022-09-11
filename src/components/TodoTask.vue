<template>
  <div
    @dblclick="$emit('toggle-reminder', task.id)"
    :class="[task.reminder ? 'reminder' : '', 'task']"
  >
    <h3>
      {{ task.text }} <span @click="$emit('delete-task', task.id)">X</span>
    </h3>
    <h3>{{ task.day }}</h3>
  </div>
</template>
<script>
export default {
  name: "TodoTask",
  props: {
    task: Object,
  },
};
</script>
<style scoped>
.task {
  background-color: #ccc;
  padding: 10px;
  margin-bottom: 5px;
}
.reminder {
  border-left: 5px solid green;
}
</style>
