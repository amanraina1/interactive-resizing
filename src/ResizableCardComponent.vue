<script setup>
import { ref } from "vue";
const startX = ref("");

const emit = defineEmits(["resize-left", "resize-right"]);

const GRID_THESHOLD = 120;

const handleResize = (e) => {
  if (startX.value - e.clientX >= GRID_THESHOLD) {
    emit("resize-left");
    startX.value = e.clientX;
  }

  if (startX.value - e.clientX <= -GRID_THESHOLD) {
    emit("resize-right");
    startX.value = e.clientX;
  }
};

const endResize = () => {
  window.removeEventListener("mousemove", handleResize);
  window.removeEventListener("mouseup", endResize);
};

const initResize = (e) => {
  e.preventDefault();
  startX.value = e.clientX;

  window.addEventListener("mousemove", handleResize);
  window.addEventListener("mouseup", endResize);
};
</script>

<template>
  <div class="card card-light h-100 w-100">
    <div class="card-header">
      <div class="card-title">hello</div>
    </div>

    <div class="card-body">This is the card content</div>

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
