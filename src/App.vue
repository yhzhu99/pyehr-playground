<template>
  <main font-sans p="x-4" text="center gray-700 dark:gray-200">
    <el-container class="flex-container">
      <el-header class="header-fixed">
        <TheHeader />
      </el-header>
      <el-main class="main-content">
        <RouterView />
      </el-main>
      <el-footer class="footer-fixed">
        <TheFooter />
      </el-footer>
    </el-container>
  </main>
</template>

<style scoped>
.flex-container {
  display: flex;
  flex-direction: column;
  height: 100vh;
}

.header-fixed {
  position: sticky;
  top: 0;
}

.main-content {
  flex-grow: 1;
  display: flex;
  justify-content: center;
  align-items: center;
}

.footer-fixed {
  position: sticky;
  bottom: 0;
}
</style>
