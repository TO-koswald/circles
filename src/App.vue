<template>
  <button @click="undo" :disabled="visibleCircles.length === 0">undo</button>
  <button @click="redo" :disabled="poppedCircles.length === 0">redo</button>
  <main @click="addCircle">
    <div
      v-for="(circle, index) in visibleCircles"
      :key="index"
      class="circle"
      :style="{ left: `${circle.x}px`, top: `${circle.y}px` }"
    >
      o
    </div>
  </main>
</template>

<script setup>
import { ref } from "vue";
const visibleCircles = ref([]);
const poppedCircles = ref([]);

function addCircle(e) {
  const { clientX: x, clientY: y } = e;
  const circle = { x, y };

  visibleCircles.value.push(circle);
}

function undo() {
  if (!visibleCircles.value.length) return;

  const poppedCircle = visibleCircles.value.pop();
  poppedCircles.value.push(poppedCircle);
}

function redo() {
  if (!poppedCircles.value.length) return;

  const circleToPush = poppedCircles.value.pop();
  visibleCircles.value.push(circleToPush);
}
</script>

<style>
body {
  margin: 0;
  padding: 0;
}

main {
  height: 100vh;
  background-color: black;
}

.circle {
  position: absolute;
  color: white;
}
</style>
