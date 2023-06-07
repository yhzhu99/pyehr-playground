<script setup lang="ts" generic="T extends any, O extends any">
defineOptions({
  name: 'IndexPage',
})
</script>

<template>
  <div class="grid-container">
    <router-link to="/performance-10fold" class="grid-item grid-item-1 button">
      <div class="content">
        <h2>Performance Table</h2>
        <p>Provides the average score across all folds</p>
      </div>
    </router-link>
    <a class="grid-item button grid-item-2" href="https://github.com/yhzhu99/pyehr" target="_blank">
      <div class="content">
        <h2>COVID-19 EHR Benchmark</h2>
        <img src="/assets/affiliations.png" alt="Project led by Peking University">
      </div>
    </a>
    <router-link to="/performance-all" class="grid-item button grid-item-3">
      <div class="content">
        <h2>Performance Table</h2>
        <p>Includes comprehensive performance details for each fold</p>
      </div>
    </router-link>
    <a class="grid-item button grid-item-4" href="https://drive.google.com/file/d/1Fdt8XUnO3CeJk9mrkPZBk_gUdpCnGFfi/view" target="_blank">
      <div class="content">
        <h2>Checkpoints & Logs</h2>
        <p>Access all model checkpoints and logs via this Google Drive link</p>
      </div>
    </a>
  </div>
</template>

<style scoped>
.grid-container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr 1fr;
  gap: 40px;
  padding: 10px;
}
.grid-item {
  width: 400px;
  height: 200px;
  padding: 20px;
  border-radius: 30px; /* adjust this to change the rounded corners */
  text-align: center;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
  transition: all 0.3s cubic-bezier(.25,.8,.25,1);
}

.content {
  text-align: center;
}

.grid-item-1 {
  grid-area: 1 / 1 / 2 / 2;
  background-color: #ffbcc2; /* red */
}

.grid-item-2 {
  grid-area: 1 / 2 / 2 / 3;
  background-color: #8fd4eb; /* orange */
}

.grid-item-3 {
  grid-area: 2 / 1 / 3 / 2;
  background-color: #aafec2; /* peach */
}

.grid-item-4 {
  grid-area: 2 / 2 / 3 / 3;
  background-color: #ffdc8b; /* green */
}

.button:hover {
  transform: scale(1.05);
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2);
  cursor: pointer;
}

.content h2 {
  font-family: 'Consolas', monospace;
  font-size: 24px;
  color: #333;
}

.content p {
  font-family: 'Consolas', monospace;
  font-size: 18px;
  color: #666;
}

.content img {
  width: 100%;
  height: auto;
}
</style>
