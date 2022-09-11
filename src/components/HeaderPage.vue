<template>
  <header>
    <h1>{{ title }}</h1>
    <ClickToActionButton
      @button-click="$emit('toggle-add-task')"
      :text="showAddTask ? 'Close' : 'Add Task'"
      :color="showAddTask ? 'red' : 'green'"
    />
  </header>
</template>
<script>
import ClickToActionButton from "./click-to-action-button.vue";

export default {
  name: "HeaderPage",
  props: {
    title: String,
    showAddTask: Boolean,
  },
  components: {
    ClickToActionButton,
  },
};
</script>
