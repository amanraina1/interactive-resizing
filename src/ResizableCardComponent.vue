<script setup>
import { reactive } from "vue";

const initialValues = reactive({
  startX: "",
  startY: "",
});

defineProps({
  title: String,
  body: String,
});
const emit = defineEmits([
  "resize-left",
  "resize-right",
  "resize-up",
  "resize-down",
]);

const GRID_THESHOLD = 120;

const handleResize = (e) => {
  if (initialValues.startX - e.clientX >= GRID_THESHOLD) {
    emit("resize-left");
    initialValues.startX = e.clientX;
  }

  if (initialValues.startX - e.clientX <= -GRID_THESHOLD) {
    emit("resize-right");
    initialValues.startX = e.clientX;
  }

  if (initialValues.startY - e.clientY >= GRID_THESHOLD) {
    emit("resize-up");
    initialValues.startY = e.clientY;
  }

  if (initialValues.startY - e.clientY <= -GRID_THESHOLD) {
    emit("resize-down");
    initialValues.startY = e.clientY;
  }
};

const endResize = () => {
  window.removeEventListener("mousemove", handleResize);
  window.removeEventListener("mouseup", endResize);
};

const initResize = (e) => {
  e.preventDefault();
  initialValues.startX = e.clientX;
  initialValues.startY = e.clientY;

  window.addEventListener("mousemove", handleResize);
  window.addEventListener("mouseup", endResize);
};
</script>

<template>
  <div class="card card-light w-100 h-100">
    <div class="card-header">
      <div class="card-title">{{ title }}</div>
    </div>

    <div class="card-body">{{ body }}</div>

    <div class="card-footer">
      <button class="btn btn-primary">Button</button>
      <span @mousedown="initResize" class="resize-handle"
        ><i class="fa-solid fa-grip-lines"></i
      ></span>
    </div>
  </div>
</template>

<style scoped>
.resize-handle {
  position: absolute;
  cursor: nw-resize;
  right: 10px;
  bottom: 0;
  transform: rotate(-150deg);
  color: lightgray;
}
</style>
