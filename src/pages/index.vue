<script setup lang="ts" generic="T extends any, O extends any">
defineOptions({
  name: 'IndexPage',
})
</script>

<template>
  <div class="button-container">
    <router-link to="/performance" class="button">
      Go to Page A
    </router-link>
    <router-link to="/predict" class="button">
      Go to Page B
    </router-link>
  </div>
</template>

<style scoped>
.button-container {
  display: flex;
  justify-content: space-around;
  width: 100%;
  height: 60vh;
  margin-bottom: 20px;
}

.button {
  padding: 20px;
  background: #f0f0f0;
  border-radius: 25px;
  color: #333;
  text-decoration: none;
  width: 40%;
  text-align: center;
  transition: background-color 0.3s ease;
}

.button:hover {
  background-color: #ddd;
}
</style>
