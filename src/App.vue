<script setup lang="ts">
import { ref } from "vue";
import logo from "./assets/SAST_Logo.png";
const n = ref(30);
const picked = ref(0);
const picking = ref(false);
let pickingInterval: number | undefined = undefined;
const pickNext = () => {
  picked.value = Math.floor(Math.random() * n.value) + 1;
};
const pickOrPause = () => {
  if (picking.value) {
    picking.value = false;
    clearInterval(pickingInterval);
  } else {
    picking.value = true;
    pickingInterval = setInterval(pickNext, 100);
  }
};
</script>

<template>
  <header>
    <img class="logo" :src="logo" alt="SAST Logo" />
    幸运抽奖系统
  </header>
  <main>
    <div class="indicator">
      最大范围：
      <input
        class="input"
        type="number"
        title="最大范围"
        v-model="n"
        placeholder="最大范围"
      />
    </div>
    <div id="display" @click="pickOrPause">
      {{ picked }}
    </div>
  </main>
</template>

<style scoped>
header {
  font-size: 5rem;
  margin-bottom: 5rem;
  height: 5rem;
}
.logo {
  height: 5rem;
}
.indicator {
  font-size: 3rem;
  display: flex;
  align-items: center;
  align-content: center;
  justify-content: center;
}
.input {
  font-size: 3rem;
  text-align: center;
  width: 50%;
  /* border: 0px; */
}
#display {
  width: 100%;
  margin: 1rem;
  display: flex;
  align-content: center;
  justify-content: center;
  font-family: monospace;
  font-size: 10rem;
}
</style>
