<script setup>
import { ref } from "vue";
import ResizableCardComponent from "./ResizableCardComponent.vue";

const widthSteps = ["col-sm-3", "col-sm-6", "col-sm-9", "col-sm-12"];
const heightSteps = ["20vh", "30vh", "40vh", "50vh"];
const cards = ref([
  {
    id: 1,
    title: "Card One",
    body: "Default 25% width text content.",
    widthIndex: 0,
    heightIndex: 0,
  },
  {
    id: 2,
    title: "Card Two",
    body: "Default 25% width text content.",
    widthIndex: 0,
    heightIndex: 1,
  },
  {
    id: 3,
    title: "Card Three",
    body: "Default 25% width text content.",
    widthIndex: 0,
    heightIndex: 2,
  },
  {
    id: 3,
    title: "Card Three",
    body: "Default 25% width text content.",
    widthIndex: 0,
    heightIndex: 3,
  },
]);

const getBootstrapedWidthClass = (size) => widthSteps[size];
const getHeightClass = (size) => heightSteps[size];

const increaseWidth = (card) => {
  if (card.widthIndex < 3) {
    card.widthIndex++;
  }
};
const decreaseWidth = (card) => {
  if (card.widthIndex > 0) {
    card.widthIndex--;
  }
};
</script>

<template>
  <div class="col-md-12 container-box p-4">
    <div class="container border rounded-3 d-flex flex-column gap-2 p-3">
      <nav class="p-2">This is my test resizabe card practical</nav>
      <div class="d-flex flex-wrap">
        <div
          class="container-body transition-width"
          :key="card.id"
          v-for="card in cards"
          :class="getBootstrapedWidthClass(card.widthIndex)"
          :style="{ height: getHeightClass(card.heightIndex) }"
        >
          <ResizableCardComponent
            :title="card.title"
            :body="card.body"
            @resize-left="decreaseWidth(card)"
            @resize-right="increaseWidth(card)"
          />
        </div>
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

.transition-width {
  transition:
    width 0.2s ease-in-out,
    flex 0.2s ease-in-out;
}
</style>
