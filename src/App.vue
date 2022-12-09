<template>
  <main @click="addCircle">
    <div
      v-for="(circle, index) in circles"
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
const circles = ref([]);

function addCircle(e) {
  const { clientX: x, clientY: y } = e;

  circles.value.push({ x, y });
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
