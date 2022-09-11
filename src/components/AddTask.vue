<template>
  <form @submit="FormSubmit" class="add-form">
    <div class="form-control">
      <label>Task</label>
      <input type="text" name="text" placeholder="Add Task" v-model="text" />
    </div>
    <div class="form-control">
      <label>Day & Time</label>
      <input type="text" name="day" placeholder="Day & Time" v-model="day" />
    </div>
    <div class="form-control">
      <label>Set Reminder</label>
      <input type="checkbox" name="reminder" v-model="reminder" />
    </div>
    <input type="submit" value="Save Task" class="btn" />
  </form>
</template>

<script>
export default {
  name: "AddTask",
  data() {
    return {
      text: "",
      day: "",
      reminder: false,
    };
  },
  methods: {
    FormSubmit(e) {
      e.preventDefault();

      if (!this.text) {
        alert("please add a task");
        return;
      }

      const newTask = {
        // id: Math.floor(Math.random() * 100000),
        text: this.text,
        day: this.day,
        reminder: this.reminder,
      };

      this.$emit("add-task", newTask);

      this.text = "";
      this.day = "";
      this.reminder = false;
    },
  },
};
</script>
<style scoped>
.form-control {
  margin-bottom: 10px;
}
.form-control input[type="text"] {
  display: block;
  height: 40px;
  box-sizing: border-box;
}
.btn {
  padding: 5px 10px;
  display: block;
  margin-bottom: 10px;
  cursor: pointer;
}
</style>
