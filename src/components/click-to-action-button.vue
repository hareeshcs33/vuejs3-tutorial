<template>
  <button @click="buttonClick()" :style="{ background: color }" class="btn">
    {{ text }}
  </button>
</template>
<script>
export default {
  name: "click-to-action-button",
  props: {
    text: String,
    color: String,
  },
  methods: {
    buttonClick() {
      this.$emit("button-click");
    },
  },
};
</script>
