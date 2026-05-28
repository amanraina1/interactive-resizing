<script setup>
import { ref, computed } from "vue";
import ResizableCardComponent from "./ResizableCardComponent.vue";

const currentIndex = ref(1);
const predefined = ["col-sm-3", "col-sm-6", "col-sm-9", "col-sm-12"];

const getComputedClass = computed(() => predefined[currentIndex.value]);

const increaseSize = () => {
  if (currentIndex.value < 3) {
    currentIndex.value++;
  }
};
const decreaseSize = () => {
  if (currentIndex.value > 0) {
    currentIndex.value--;
  }
};
</script>

<template>
  <div class="col-md-12 container-box p-4">
    <div class="container border rounded-3 d-flex flex-column gap-2 p-3">
      <nav class="p-2">This is my test resizabe card practical</nav>
      <div
        class="container-body d-flex flex-wrap gap-3"
        :class="getComputedClass"
      >
        <ResizableCardComponent
          @resize-left="decreaseSize"
          @resize-right="increaseSize"
        />
      </div>
    </div>
  </div>
</template>

<style scoped>
nav {
  min-height: 50px;
  background-color: lightblue;
  margin-bottom: 100px;
  border-radius: 10px;
}
.container-box {
  height: 100vh;
}

.container {
  height: 100%;
}
</style>
